# ⚠️ Node.js Not Installed

## The Problem
You're seeing `ERR_CONNECTION_REFUSED` because **Node.js is not installed** on your computer. The app needs Node.js to run.

## ✅ Solution: Install Node.js

### Step 1: Download Node.js
1. Go to: **https://nodejs.org/**
2. Download the **LTS version** (recommended, e.g., v20.x.x or v18.x.x)
3. Choose the **Windows Installer (.msi)** for your system (64-bit or 32-bit)

### Step 2: Install Node.js
1. Run the downloaded installer
2. Click "Next" through the installation wizard
3. **Important:** Make sure "Add to PATH" is checked ✅
4. Click "Install"
5. Wait for installation to complete
6. Click "Finish"

### Step 3: Verify Installation
1. **Close and reopen your terminal/command prompt** (important!)
2. Run these commands:
   ```bash
   node --version
   npm --version
   ```
   
   You should see version numbers like:
   ```
   v20.11.0
   10.2.4
   ```

### Step 4: Install Project Dependencies
Once Node.js is installed, come back here and run:

```bash
cd "c:\Users\ryans\OneDrive\New folder"
npm run install:all
```

This will install all dependencies for both backend and frontend.

### Step 5: Setup Database
Make sure PostgreSQL is installed and running, then:

```bash
cd backend
npm run db:generate
npm run db:push
cd ..
```

### Step 6: Start the App
```bash
npm run dev
```

## Alternative: Use Node Version Manager (nvm-windows)

If you prefer using a version manager:

1. Download nvm-windows: https://github.com/coreybutler/nvm-windows/releases
2. Install nvm-windows
3. Open a new terminal and run:
   ```bash
   nvm install lts
   nvm use lts
   ```

## After Installing Node.js

Once Node.js is installed:
1. **Restart your terminal/VS Code** (very important!)
2. Navigate to the project folder
3. Run `npm run install:all`
4. Then run `npm run dev`

## Need Help?

- Node.js website: https://nodejs.org/
- Node.js documentation: https://nodejs.org/docs/
- If you have issues, make sure to restart your terminal after installing!
