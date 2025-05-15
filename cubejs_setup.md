# Cube.js Setup Guide

## Part 1: Install Cube.js CLI & Initialize Project

### 1. Install Cube.js CLI globally

```bash
npm install -g cubejs-cli
```

### 2. Create a new Cube.js project

```bash
cubejs create ksproject-cube -d postgres
```

This creates a folder named `ksproject-cube` with the basic structure.

#### 📁 Project Structure Overview

```
ksproject-cube/
├── .env
├── package.json
├── cube.js
├── schema/
│   └── <your cubes>.js
├── model/                # (if you use CUBEJS_SCHEMA_PATH=model)
│   └── <your cubes>.js
├── docker-compose.yml
└── ...
```

---

## 🛠️ Part 2: Configure Environment Variables (`.env`)

Create or edit `.env` in the root of your Cube.js project:

```ini
# Developer mode
CUBEJS_DEV_MODE=true

# Database source (Airbyte-connected Postgres)
CUBEJS_DB_TYPE=postgres
CUBEJS_DB_HOST=localhost
CUBEJS_DB_NAME=ksproject
CUBEJS_DB_USER=airbyte_user
CUBEJS_DB_PASS=password
CUBEJS_DB_PORT=5432

# Cube.js settings
CUBEJS_API_SECRET=your-secure-random-api-secret
CUBEJS_EXTERNAL_DEFAULT=true
CUBEJS_SCHEDULED_REFRESH_DEFAULT=true
CUBEJS_SCHEMA_PATH=model
CUBEJS_WEB_SOCKETS=true
#CUBEJS_SCHEMA_EXTENSION=yml

# Cube Store PostgreSQL-like SQL API
CUBEJS_PG_SQL_PORT=15432
CUBEJS_SQL_USER=admin
CUBEJS_SQL_PASSWORD=admin
```

> **🔐 Replace with your real DB and secure values.**

---

## 📦 Part 3: Install Dependencies

```bash
cd ksproject-cube
npm install
```

### Optional: Run with Docker

If using Docker, update `docker-compose.yml` and run:

```bash
docker-compose up
```

---

## 🧱 Part 4: Create a Cube (Data Model)

By default, cubes go in the `schema/` folder. If you set `CUBEJS_SCHEMA_PATH=model`, use the `model/` folder instead.

### Example: Create a cube from `orders` table

1. Create `model/Orders.js` (or `schema/Orders.js` if default path):

```js
cube(`Orders`, {
    sql: `SELECT * FROM public.orders`,

    measures: {
        count: {
            type: `count`,
            drillMembers: [id, createdAt],
        },
    },

    dimensions: {
        id: {
            sql: `id`,
            type: `number`,
            primaryKey: true,
        },

        status: {
            sql: `status`,
            type: `string`,
        },

        createdAt: {
            sql: `created_at`,
            type: `time`,
        },
    },
});
```

✅ You can run the following to generate cubes:

```bash
npx cubejs-cli generate -t orders
```

---

## ▶️ Part 5: Start Cube.js

```bash
npm run dev
```

Visit [http://localhost:4000](http://localhost:4000)  
Explore data in the Developer Playground (enabled in dev mode).

---

## 🧪 Verify Cube.js is Working

Check API:

```bash
curl -H "Authorization: your-secure-random-api-secret" http://localhost:4000/cubejs-api/v1/meta
```