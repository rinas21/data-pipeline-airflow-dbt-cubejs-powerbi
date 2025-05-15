# Connecting Power BI to Cube.js via PostgreSQL (Cube Store)

Follow these steps to connect Power BI to your Cube.js analytics backend and start building dashboards:

---

## ✅ Step-by-Step Guide

### 1. Open Power BI
Launch **Power BI Desktop**.

### 2. Click on Get Data
In the top menu, click the **Get Data** icon.

### 3. Search and Select PostgreSQL Database
- In the search bar, type `PostgreSQL`.
- Select **PostgreSQL database** from the list.

### 4. Enter Connection Info
In the dialog box, enter:
- **Server:** `IP_ADDRESS:15432` (e.g., `localhost:15432`)
- **Database:** Your Cube.js project DB name (e.g., `ksproject`)

> **Note:**  
> Make sure Cube.js is running and `CUBEJS_PG_SQL_PORT=15432` is set in `.env`.

### 5. Choose Import as Data Connectivity Mode
- Select the **Import** option (not DirectQuery).
- Click **OK**.

### 6. Select Views from Navigator
- The Navigator window will load available views.
- Select the desired view(s) to import data from.
- Click **Load** and wait for Power BI to finish importing.

### 7. Start Building the Dashboard
- Once loaded, your data will appear in the **Fields** pane.
- Use visualizations, charts, slicers, and more to start building your dashboard.

---

## 📝 Notes

- Ensure that Cube.js is running and listening on port `15432`.
- Your `.env` should contain:

    ```env
    CUBEJS_PG_SQL_PORT=15432
    CUBEJS_SQL_USER=admin
    CUBEJS_SQL_PASSWORD=admin
    ```

- If you get connection errors, make sure Cube Store is running, and the port is not blocked by a firewall.

---

> **Tip:**  
> For best results, always use the **Import** mode in Power BI when connecting to Cube.js via PostgreSQL.
