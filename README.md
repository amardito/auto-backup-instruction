
# Antares Eazy – Auto Backup Cloud Recording (On-Prem CLI)

This CLI tool helps you **automate backup of CCTV recordings** from Antares Eazy into your on-premise environment.

---

## 🚀 Prerequisites

Before installation, ensure you are running **Windows with PowerShell (Administrator mode)**.

### 🧰 Step 1: Install Chocolatey (Windows Package Manager)
Open PowerShell as Administrator, then run:

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; `
[System.Net.ServicePointManager]::SecurityProtocol = `
[System.Net.ServicePointManager]::SecurityProtocol -bor 3072; `
iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

This installs Chocolatey so you can easily install Docker and other tools.

---

### 🐳 Step 2: Install Docker with Chocolatey
Once Chocolatey is installed, run: 

- **Powershell**  
```
choco install docker-desktop -y
```

After installation:
- Restart your system
- Launch Docker Desktop
- Make sure Docker is running (check the whale icon in the system tray)

---

### 📦 Step 3: Initialize and Run Your Service with Docker

first go to folder directory auto-backup then
request .env file to operator and put the file on service directory

run docker engine
```
Start-Process "C:\Program Files\Docker\Docker\Docker Desktop.exe"
```

request app to operator

open terminal on directory app which is antares-eazy-auto-backup-cloud-recording

also need request .env to operator to save in directory app

then open in terminal the service directory, and run this:
```
docker compose build
docker compose run auto-backup
```

### 👁️ Step 4: Watching worker

run this docker command

```
docker compose run auto-backup sh
```

run this after /app open
```
tail -f /logs/worker.log
```



