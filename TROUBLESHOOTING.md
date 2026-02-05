# Troubleshooting Guide

## Issue: App redirects to Google or shows "localhost refused to connect"

### What I Fixed:
1. ✅ Removed Google OAuth buttons from Login and Register pages
2. ✅ Made backend Google OAuth routes return errors instead of redirecting when credentials aren't configured
3. ✅ Prevented Passport from initializing Google strategy without credentials

### How to Run the App:

1. **Make sure both servers are running:**
   ```bash
   npm run dev
   ```
   This starts:
   - Frontend on http://localhost:5173
   - Backend on http://localhost:3001

2. **Open your browser to:**
   ```
   http://localhost:5173
   ```

3. **Clear your browser cache:**
   - Press `Ctrl+Shift+Delete` (Windows) or `Cmd+Shift+Delete` (Mac)
   - Clear cached images and files
   - Or use Incognito/Private browsing mode

4. **If you still see Google redirect:**
   - Check your browser's address bar - make sure you're on `localhost:5173` not `localhost:3001`
   - Check browser console (F12) for any errors
   - Make sure you're not clicking any "Google" buttons (they should be removed)

### Using the App:

1. **Register a new account:**
   - Go to http://localhost:5173/register
   - Fill in email, password, display name, and role
   - Click "Sign Up"

2. **Login:**
   - Go to http://localhost:5173/login
   - Enter email and password
   - Click "Sign In"

### If Backend Isn't Running:

If you see "localhost refused to connect" when trying to login/register:

1. Check if backend is running:
   ```bash
   cd backend
   npm run dev
   ```

2. Check backend logs for errors

3. Make sure `.env` file exists in `backend/` folder with:
   ```
   DATABASE_URL="postgresql://..."
   JWT_SECRET="your-secret-key"
   PORT=3001
   FRONTEND_URL=http://localhost:5173
   ```

### Still Having Issues?

1. **Check browser console (F12):**
   - Look for any red errors
   - Check Network tab to see which requests are failing

2. **Check terminal/console:**
   - Look for backend errors
   - Make sure database is running (PostgreSQL)

3. **Try a fresh start:**
   ```bash
   # Stop all running processes (Ctrl+C)
   # Then restart
   npm run dev
   ```

4. **Verify you're using the right URL:**
   - Frontend: http://localhost:5173
   - Backend API: http://localhost:3001/api
