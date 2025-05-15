# 🧩 Installing and Running Airbyte with `abctl` (Mac & Linux)

## 🚀 Part 1: Install `abctl`

### ✅ Fast Installation (Recommended)
Open a terminal and run:
```bash
curl -LsfS https://get.airbyte.com | bash -
```
> **Note:** You may be prompted for your password.

If successful, you will see:
```
abctl install succeeded
```

---

### ⚙️ Manual Installation

1. **Verify Architecture**
    ```bash
    uname -m
    ```
    - Output `x86_64` → Download `linux-amd64` version  
    - Output `aarch64` → Download `linux-arm64` version

2. **Download and Extract**
    ```bash
    tar -xvzf {name-of-file-downloaded.linux-*.tar.gz}
    ```

3. **Make Executable & Move to PATH**
    ```bash
    chmod +x abctl/abctl
    sudo mv abctl /usr/local/bin
    ```

4. **Verify Installation**
    ```bash
    abctl version
    ```

---

## 🐳 Part 2: Run Airbyte

**Prerequisite:**  
Ensure Docker Desktop is running.

### 🧱 Install Airbyte (Standard)
```bash
abctl local install
```

### 🧱 Install Airbyte (Low-resource mode)
```bash
abctl local install --low-resource-mode
```

> ⚠️ **Warning:**  
> If you see `Readiness probe failed: HTTP probe failed with statuscode: 503`,  
> you may need more system resources, but installation will complete.

⏳ Installation may take up to 15 minutes.  
Once complete, open: [http://localhost:8000](http://localhost:8000)

---

## 🔐 Part 3: Set Up Authentication

### Get Default Credentials
```bash
abctl local credentials
```
**Example Output:**
```
Credentials:
Email: user@example.com
Password: random_password
Client-Id: 03ef466c-5558-4ca5-856b-4960ba7c161b
Client-Secret: m2UjnDO4iyBQ3IsRiy5GG3LaZWP6xs9I
```
Login to [http://localhost:8000](http://localhost:8000) using the credentials above.

---

### 🔁 (Optional) Change Your Password
```bash
abctl local credentials --password YourStrongPasswordExample
```
> Your Airbyte server will restart with the new password.

---

**Note:**  
- Always keep your credentials secure.
- For more details, refer to the [Airbyte documentation](https://docs.airbyte.com/).