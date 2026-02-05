# Verify Node.js Installation

## Did you install Node.js or just download it?

**Downloading ≠ Installing!**

If you only **downloaded** the installer but haven't **run it yet**, you need to:

1. Find the downloaded file (usually in Downloads folder)
2. Double-click the `.msi` file
3. Follow the installation wizard
4. Make sure "Add to PATH" is checked ✅
5. Click "Install"
6. Wait for it to finish
7. **Restart VS Code completely**

## After Installing:

### Option 1: Restart VS Code
1. Close ALL VS Code windows
2. Reopen VS Code
3. Open a new terminal (Ctrl + `)
4. Try: `node --version`

### Option 2: Use Windows Command Prompt
1. Press `Win + R`
2. Type `cmd` and press Enter
3. Try: `node --version`
4. If it works here, VS Code terminal needs to be restarted

### Option 3: Check Installation Path
Node.js is usually installed to:
- `C:\Program Files\nodejs\`
- Or `C:\Program Files (x86)\nodejs\`

Check if these folders exist. If they do, Node.js is installed but PATH might not be updated.

## Quick Test:

Open **Windows Command Prompt** (not VS Code terminal) and run:
```cmd
node --version
npm --version
```

If this works in Command Prompt but not VS Code:
- VS Code needs to be restarted
- Or VS Code terminal is using a different shell

## Still Not Working?

1. **Reinstall Node.js:**
   - Go to https://nodejs.org/
   - Download the LTS version again
   - Run the installer
   - Make sure "Add to PATH" is checked
   - Restart your computer (sometimes needed)

2. **Manual PATH check:**
   - Press `Win + X` → System → Advanced system settings
   - Click "Environment Variables"
   - Under "System variables", find "Path"
   - Check if `C:\Program Files\nodejs\` is listed
   - If not, add it manually

3. **Try PowerShell instead:**
   - In VS Code, open terminal
   - Click the dropdown next to "+"
   - Select "PowerShell" or "Command Prompt"
   - Try `node --version` again
