## 1. Install MySQL Workbench on Arch Linux

**Recommended way (AUR):**
```bash
paru -S mysql-workbench
# or (if using yay)
yay -S mysql-workbench
```

_If you need to install dependencies, follow any prompts._

## 2. Start MySQL Server

If you haven’t already installed MySQL/MariaDB:
```bash
paru -S mariadb  # or mysql
sudo mariadb-install-db --user=mysql --basedir=/usr --datadir=/var/lib/mysql
sudo systemctl enable mariadb
sudo systemctl start mariadb
```
_You can use MariaDB as a drop-in replacement for MySQL: MySQL Workbench works with both!_

## 3. Launch MySQL Workbench

- Run `mysql-workbench` from your applications menu or terminal.

## 4. Set Up a New Connection

1. **Click the `+` next to "MySQL Connections"** on the main screen.
2. **Enter Connection Details:**
   - **Connection Name:** (e.g., `Local MariaDB`)
   - **Hostname:** `127.0.0.1` (or `localhost`)
   - **Port:** `3306`
   - **Username:** `root` (or your database user)
   - **Password:** Click "Store in Vault" and enter your root password.

3. **Test Connection** to make sure it works, then click "OK".

## 5. Import and Run SQL Script

1. **Open your SQL file:**
   - Go to `File > Open SQL Script…`
   - Select your `cape_town_infrastructure.sql` file.

2. **Select a Connection/Database:**
   - Make sure you’re connected to your server.
   - If the database (`CapeTownInfrastructure`) doesn’t exist yet, the script will create it.

3. **Execute Script:**
   - Click the **lightning bolt** (“Execute the selected portion of the script”).
   - You can run the whole script or highlight specific sections to run.

## 6. View Data and Run Queries

- Use the SCHEMAS sidebar to browse your database and tables.
- Open a new SQL tab to run queries (e.g., your SELECT statement).

## 7. Example Workflow

- Open `cape_town_infrastructure.sql` in Workbench.
- Click Execute.
- Refresh the SCHEMAS sidebar to see your new tables and data.
- Run additional queries as needed.

---

### Troubleshooting

- If you get connection errors:
  - Ensure MySQL/MariaDB is running: `sudo systemctl status mariadb`
  - Check the port and credentials.
- MariaDB is fully compatible for standard SQL commands in Workbench.

---

