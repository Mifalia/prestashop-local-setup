# PrestaShop 1.7.6.8 — Local Docker Setup

## Stack

| Container | Image                         | Port host |
| --------- | ----------------------------- | --------- |
| `ps`      | prestashop/prestashop:1.7.6.8 | `5300`    |
| `pspma`   | phpmyadmin/phpmyadmin:5.2.2   | `5301`    |
| `psdb`    | mysql:5.7                     | `5306`    |

---

## Prerequisites

- Docker Desktop or just Docker on a Linux based OS

---

## Setup

**1. Clone the project**

```bash
git clone https://github.com/Mifalia/prestashop-local-setup.git
```

**2. Configure `.env`**

```bash
cp .env.example .env
# adjust based on your personal preferences
```

**3. Start the stack**

```bash
docker-compose up -d
docker logs -f ps  # only if you want to follow installation process step by step (idk this will take like ~2-3 mins, not more (I hope :))
```

**4. Proceed to Prestashop installation** on `http://localhost:5300/install`

---

## Access the panel

| URL                                 | Creds                                           |
| ----------------------------------- | ----------------------------------------------- |
| `http://localhost:5300`             | —                                               |
| `http://localhost:5300/admin_local` | `PS_ADMIN_MAIL` / `PS_ADMIN_PASSWD` from `.env` |
| `http://localhost:5300`             | root / `MYSQL_ROOT_PASSWORD` from `.env`        |

---

## Dev (VS Code)

`Ctrl+Shift+P` → **Dev Containers: Attach to Running Container** → `/ps` → open `/var/www/html`

---

## Useful commands

```bash
docker-compose up -d          # start
docker-compose down           # stop
docker-compose down -v        # drop everything
docker exec -it ps bash       # open prestashop container fs
```

## Bonus

- You can configure a nginx reverse-proxy to access the prestashop within a local domain name + https enabled. All you have to do is redirect the incoming traffic to port `80` of `ps` and `pma` and use the service name on `proxy_pass`. (THIS IS THE BEST OPTION TO FINALIZE THE SETUP)

- Use Vscode "Dev Containers" extension (authored by microsoft) for a comfortable development experience.
