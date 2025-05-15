# dbt (Postgres Adapter) Setup Guide

## Part 1: Install dbt (Postgres Adapter)

### For Mac/Linux (Using pipx – Recommended)
```bash
# If pipx is not installed
python3 -m pip install --user pipx
python3 -m pipx ensurepath

# Install dbt for PostgreSQL
pipx install dbt-postgres
```

**Alternatively, using pip:**
```bash
pip install dbt-postgres
```

### Verify Installation
```bash
dbt --version
```

---

## Part 2: Set Up dbt Profile

dbt uses a `profiles.yml` file located at `~/.dbt/profiles.yml`.

**Create the `.dbt` directory if it doesn't exist:**
```bash
mkdir -p ~/.dbt
```

**Sample `profiles.yml` for PostgreSQL:**
```yaml
my_dbt_project:
    target: dev
    outputs:
        dev:
            type: postgres
            host: localhost  # or your remote DB host
            user: your_db_user
            password: your_db_password
            port: 5432
            dbname: your_database_name
            schema: analytics  # your target schema in PostgreSQL
            threads: 4
            keepalives_idle: 0
            sslmode: prefer
```
> **Note:** Replace `your_db_user`, `your_db_password`, and other values as needed.

---

## Part 3: Create a New dbt Project

```bash
dbt init my_dbt_project
```

This creates a structure like:
```
my_dbt_project/
├── dbt_project.yml
├── models/
│   └── example/
│       └── my_first_dbt_model.sql
├── macros/
└── ...
```
When prompted for the profile name, enter the same name you used in `profiles.yml` (e.g., `my_dbt_project`).

---

## Part 4: Configure dbt Project

Edit the `dbt_project.yml` in your project folder:
```yaml
name: 'my_dbt_project'
version: '1.0.0'
config-version: 2

profile: 'my_dbt_project'  # Must match the name in profiles.yml

model-paths: ["models"]
analysis-paths: ["analysis"]
test-paths: ["tests"]
macro-paths: ["macros"]
target-path: "target"
clean-targets: ["target", "dbt_modules"]
```

---

## Part 5: Test Your Setup

1. Navigate to your project:
        ```bash
        cd my_dbt_project
        ```
2. Test Connection:
        ```bash
        dbt debug
        ```
        You should see a success message if everything is correctly set up.

---

## Part 6: Run Your Models

```bash
dbt run
```
This compiles and runs the SQL models in your `models/` folder into your PostgreSQL schema.

---
