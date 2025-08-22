# install choco

Run this on powershell with administrator

```
Set-ExecutionPolicy Bypass -Scope Process -Force; `
[System.Net.ServicePointManager]::SecurityProtocol = `
[System.Net.ServicePointManager]::SecurityProtocol -bor 3072; `
iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

Close and reopen powershell with administrator
then run

```
choco -v
```


# Install onprem environment

- Node.js LTS (includes npm)
```
choco install nodejs-lts --version=18.20.2 -y
```
- Redis
```
choco install redis -y
cd "C:\ProgramData\chocolatey\lib\redis\tools"
.\redis-server.exe --service-install redis.windows.conf
.\redis-server.exe --service-start
Set-Service -Name redis -StartupType Automatic
```
- Mysql
```
choco install mysql -y
```
- ffmpeg (for video conversion)
```
choco install ffmpeg -y
```

Close and reopen powershell with administrator

## Environment requirement check
```
node -v
```
```
npm -v
```
```
Get-Service redis
```
```
mysql --version
```
```
ffmpeg -version
```

## Installation APP
```
unzip antares-eazy-auto-backup-cloud-recording.zip
cd antares-eazy-auto-backup-cloud-recording
```
open powershell and goto dir folder app
```
copy .env.example .env
```
Request .env value to Operator
```
npm install
```

## setup database environment
```
mysql -u root -p
```

press enter without password

```
CREATE DATABASE onprem_backup CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

write "exit" then press enter


# How to use Onprem

1. open powershell and goto dir folder app
run this command
```
npx onprem-backup login
```
after ✔️ success login
exit terminal with ctrl+c 2x

2. still in terminal on dir folder app
run this command
```
npx onprem-backup select-camera
```
select camera with arrow up and down key
and press "space" to selecting camera or press "a" to selecting all camera
and press enter
after ✔️ success selecting camera
exit terminal with ctrl+c 2x

3. still in terminal on dir folder app
run this command to schedule download 2 hour back from now
```
npx onprem-backup schedule
```
or
run this command to schedule download with custom time from now
```
npx onprem-backup schedule --from epochTime
```
you can get epochTime from here [epochTimeConverter](https://www.unixtimestamp.com/)

4. open new terminal and goto dir folder app
then run this, to run auto download
```
npm run worker
```

## COMMAND LIST

- npx onprem-backup login
- npx onprem-backup select-camera
- npx onprem-backup schedule
- npm run worker
