# Swift Postgres

Local PostgreSQL development environment powered by Docker Compose.

## Requirements

- Docker Desktop
- A PostgreSQL UI client such as pgAdmin, DBeaver, TablePlus, or DataGrip

## First-Time Setup

Copy the example environment file and adjust any values you want to change:

```powershell
Copy-Item .env.example .env
```

Start Postgres and pgAdmin:

```powershell
docker compose up -d
```

Check container status:

```powershell
docker compose ps
```

## Connection Details

From tools running on your host machine:

- Host: `localhost`
- Port: `5432`
- Database: `appdb`
- Username: `appuser`
- Password: `change-me`

pgAdmin is available at:

- URL: `http://localhost:5050`
- Email: `admin@example.com`
- Password: `change-me`

When registering the database server inside pgAdmin, use these settings:

- Host name/address: `postgres`
- Port: `5432`
- Maintenance database: `appdb`
- Username: `appuser`
- Password: `change-me`

The hostname is `postgres` inside pgAdmin because both containers run on the same Docker Compose network.

## Database Initialization

SQL files in `db/init` run automatically only when the Postgres data volume is created for the first time. If you add or change init scripts after the database already exists, recreate the volume:

```powershell
docker compose down -v
docker compose up -d
```

This deletes the local database volume, so only use it when you are comfortable losing local data.

## Common Commands

Stop containers:

```powershell
docker compose down
```

View logs:

```powershell
docker compose logs -f
```

Open a `psql` shell inside the Postgres container:

```powershell
docker compose exec postgres psql -U appuser -d appdb
```
