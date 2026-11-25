# Runbook: deploy the database stack

**When to use:** first deployment of `stacks/databases`, or redeploying after a change.
**Time:** about 20 minutes the first time.

## 1. Remove the old CasaOS database apps (first time only)

The CasaOS app-store versions of MariaDB, PostgreSQL and Adminer use the same ports (3306, 5432, 8080), so they must go first. They hold no data worth keeping yet.

In the CasaOS dashboard, uninstall MariaDB, PostgreSQL and Adminer. Then check nothing is still listening:

```bash
sudo ss -ltnp | grep -E ':(3306|5432|8080)\s' || echo "ports free"
```

## 2. Get the repository onto the server (first time only)

```bash
sudo apt install -y git
cd ~ && git clone https://github.com/fatherlanding/homelab-gitops.git
```

## 3. Create the secrets file

```bash
cd ~/homelab-gitops/stacks/databases
cp .env.example .env
nano .env        # replace every change-me; generate passwords with: openssl rand -base64 24
chmod 600 .env
```

## 4. Start the stack

```bash
docker compose up -d
docker compose ps
```

Wait until all three show `running`, and MariaDB and PostgreSQL show `(healthy)`. That takes up to a minute.

## 5. Check it worked

| Check | How | Expected |
|---|---|---|
| Adminer opens | Browser: `http://<server-ip>:8080` | Login page, server pre-filled as `mariadb` |
| MariaDB login | Adminer: System MySQL, server `mariadb`, your MARIADB_USER | Database `olist` listed |
| PostgreSQL login | Adminer: System PostgreSQL, server `postgres`, your POSTGRES_USER | Database `practice` listed |
| From the Windows PC | DBeaver, MariaDB connection to `<server-ip>:3306` | Connects |

## Updating later

```bash
cd ~/homelab-gitops && git pull
cd stacks/databases && docker compose up -d
```

## If something goes wrong

- `port is already allocated`: an old CasaOS app still holds the port; repeat step 1.
- `set MARIADB_ROOT_PASSWORD in .env`: the `.env` file is missing or a value is blank; repeat step 3.
- Container keeps restarting: `docker compose logs mariadb` (or `postgres`) shows why.
