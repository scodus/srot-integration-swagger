# SROT Integration swagger
URL : https://scodus.github.io/srot-integration-swagger/

---
### Postman → Swagger UI on Windows 11

### Overview

This guide helps you:

1. Set up required tools: Chocolatey, Make, Node.js, NVM.
2. Convert a Postman collection JSON into Swagger/OpenAPI YAML.
3. Serve the Swagger/OpenAPI specification using Swagger UI locally.

---

### Step 1: Install Chocolatey (Windows package manager)

Open PowerShell as Administrator and run:

```
Set-ExecutionPolicy Bypass -Scope Process -Force
[System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072
iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

Close and reopen PowerShell. Test installation:

```
choco -v
```

---

### Step 2: Install Make

```
choco install make
```

Test:

```
make --version
```

---

### Step 3: Install Node.js 18

#### Option A — Direct Node.js Installer

1. Download Node.js LTS 18.x Windows Installer (.msi) from [https://nodejs.org/en/download/](https://nodejs.org/en/download/)
2. Run the installer and follow prompts.
3. Test installation:

```
node -v
npm -v
```

#### Option B — NVM for Windows (Recommended)

1. Install NVM for Windows: [https://github.com/coreybutler/nvm-windows](https://github.com/coreybutler/nvm-windows)
2. Install Node 18:

```
nvm install 18.17.1
nvm use 18
node -v
```

3. Optional: set Node 18 as default:

```
nvm alias default 18
```

> Using NVM allows switching between multiple Node versions.

---

### Step 4: Install `postman-to-openapi`

#### Option A — Global Install

```
npm install -g postman-to-openapi
```

Make sure the Node 18 global `.bin` folder is in your PATH:

```
C:\Users\acer\AppData\Local\nvm\v18.17.1\node_modules\.bin
```

Test:

```
postman-to-openapi --version
```

#### Option B — Using npx (No PATH issues)

```
npx postman-to-openapi collection.json swagger.yaml -f
```

* `collection.json` → Postman collection file
* `swagger.yaml` → output OpenAPI file
* `-f` → overwrite if exists

---

### Step 5: Convert Postman Collection to Swagger/OpenAPI

```
postman-to-openapi collection.json swagger.yaml -f
```

or using npx:

```
npx postman-to-openapi collection.json swagger.yaml -f
```

✅ Creates `swagger.yaml` from your Postman collection.

---


### Optional: One-line automation

```
npx postman-to-openapi collection.json swagger.yaml -f; node server.js
```

> Converts Postman → Swagger and starts Swagger UI server in one step.

---

### Notes

* Node Compatibility: `postman-to-openapi` works reliably on Node 18. Node 19+ may fail.
* NVM vs Direct Node: Use NVM if switching Node versions often. Use direct installer for simplicity.
* npx Usage: Avoids PATH issues; recommended with NVM.
* Swagger UI: Can be customized via downloaded Swagger UI and linking `swagger.yaml`.

This setup is fully Windows 11 compatible and works with NVM, Node 18, Make, Chocolatey, and Postman collections.
