# PostgreSQL Configuration & Cube.js Integration Guide (Ubuntu)

## 📁 Important PostgreSQL Files in `/postgresql/17/main/`

| File Name         | Description                                                                 |
|-------------------|-----------------------------------------------------------------------------|
| `postgresql.conf` | Main PostgreSQL configuration file (e.g., port, logging, memory settings).   |
| `pg_hba.conf`     | Controls client authentication (who can connect, from where, and how).       |
| `pg_ident.conf`   | Maps OS users to DB users (used with ident method).                          |
| `environment`     | Environment variable definitions for PostgreSQL.                             |
| `start.conf`      | Used to define if the cluster should auto-start.                             |
| `pg_ctl.conf`     | Control file used by `pg_ctl` command for managing PostgreSQL.               |
| `conf.d/`         | Directory for additional configuration files (included in `postgresql.conf`).|

---

## 👤 Step-by-Step: Create PostgreSQL User for Cube.js

You’ll use these credentials in your `.env` file for Cube.js:

```env
CUBEJS_DB_USER=airbyte_user
CUBEJS_DB_PASS=password
CUBEJS_DB_NAME=ksproject
```

### 1. Access the PostgreSQL Shell

```bash
sudo -u postgres psql
```

### 2. Create the User and Database

```sql
-- Create user
CREATE USER airbyte_user WITH PASSWORD 'password';

-- Create database
CREATE DATABASE ksproject OWNER airbyte_user;

-- Grant privileges
GRANT ALL PRIVILEGES ON DATABASE ksproject TO airbyte_user;
```
> **Note:** Replace `password` with a secure password.

---

## 🔒 Configure `pg_hba.conf`

Edit the file:

```bash
sudo nano /postgresql/17/main/pg_hba.conf
```

Add the following line at the top or before any `host` entries:

```conf
# Allow local connections with password
host    all             all             127.0.0.1/32            md5
```

Save and exit (`Ctrl+O`, then `Enter`, then `Ctrl+X`).

---

## ⚙️ Configure `postgresql.conf`

Edit the config file:

```bash
sudo nano /postgresql/17/main/postgresql.conf
```

Ensure these settings are set:

```conf
listen_addresses = 'localhost'
port = 5432
```
> Only use `localhost` unless allowing external access.

---

## 🔁 Restart PostgreSQL to Apply Changes

```bash
sudo systemctl restart postgresql
```

To check if PostgreSQL is running:

```bash
sudo systemctl status postgresql
```

---

## ✅ Final Check for Cube.js Compatibility

Ensure your `.env` file for Cube.js includes:

```env
CUBEJS_DB_TYPE=postgres
CUBEJS_DB_HOST=localhost
CUBEJS_DB_PORT=5432
CUBEJS_DB_NAME=ksproject
CUBEJS_DB_USER=airbyte_user
CUBEJS_DB_PASS=password
```

To verify the connection:

```bash
psql -U airbyte_user -d ksproject -h 127.0.0.1 -W
```