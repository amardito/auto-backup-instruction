
# Antares Eazy – Auto Backup Cloud Recording (On-Prem CLI)

This CLI tool helps you **automate backup of CCTV recordings** from Antares Eazy into your on-premise environment.

---

## 🚀 Prerequisites

Before installation, ensure you are running **Windows with PowerShell (Administrator mode)**.

### 1. Install Chocolatey  
Run the following command in **PowerShell (Admin):**

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; `
[System.Net.ServicePointManager]::SecurityProtocol = `
[System.Net.ServicePointManager]::SecurityProtocol -bor 3072; `
iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

Close and reopen PowerShell (Admin), then verify installation:

```powershell
choco -v
```

---

### 2. Install Dependencies via Chocolatey  

- **Node.js LTS (v18.20.2)**  
```powershell
choco install nodejs-lts --version=18.20.2 -y
```

- **Redis**  
```powershell
choco install redis -y
```

- **MySQL (or MariaDB alternative)**  
```powershell
choco install mysql -y
# If MySQL fails, try:
choco install mariadb -y
```

- **FFmpeg (for video conversion)**  
```powershell
choco install ffmpeg -y
```

Reopen PowerShell (Admin) after installation.

---

## ✅ Verify Environment Setup  

Run the following commands to confirm everything is installed:

```powershell
node -v
npm -v
redis-server
mysql --version
ffmpeg -version
```

⚠️ Keep `redis-server` running in a dedicated terminal.

---

## 📦 Install the App

1. Extract the package:
```powershell
unzip antares-eazy-auto-backup-cloud-recording.zip
cd antares-eazy-auto-backup-cloud-recording
```

2. Copy environment file:
```powershell
copy .env.example .env
```

🔑 Request `.env` values from the Operator.  

3. Install dependencies:
```powershell
npm install
```
do this while in directory antares-eazy-auto-backup-cloud-recording

---

## 🗄️ Database Setup  

1. Open MySQL (press **Enter** if no password):  
```powershell
mysql -u root -p
```

2. Create the database:  
```sql
CREATE DATABASE onprem_backup CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

3. Exit MySQL:  
```sql
exit
```

---

## 📘 Usage Guide  

```powershell
npx onprem-backup
```

### 1. Login with Antares Eazy Account  
```powershell
login
```

### 2. Select Camera(s)  
```powershell
select-camera
```
- Use `↑ / ↓` keys to navigate.  
- Press `Space` to select.  
- Press `a` to select **all cameras**.  
- Press `Enter` to confirm.  

### 3. Schedule Auto Download  

- Download last **2 hours**:  
```powershell
schedule
```
Download range time with **custom epoch time**:  
👉 Convert time to epoch here: [Unix Timestamp Converter](https://www.unixtimestamp.com/)

### 4. Run Auto Download Worker  
In a **new terminal**, run:  
```powershell
npm run worker
```

---

## 📜 Command Reference  

| Command                                | Description                         |
|----------------------------------------|-------------------------------------|
| `npx onprem-backup`                    | Antares Eazy CLI auto backup        |
| `redis-server`                         | Job manager auto-download           |
| `npm run worker`                       | Start the worker for auto-download  |

---
