# 🚀 How to Start BrandLink

## The Issue
You're seeing **"ERR_CONNECTION_REFUSED"** because the backend server isn't running.

## ✅ I Just Fixed:
1. Created `backend/.env` file (was missing!)
2. Disabled Google OAuth to prevent redirect issues

## 📋 Steps to Start:

### 1. **Update Database Connection**
   Open `backend/.env` and update the `DATABASE_URL` line:
   ```env
   DATABASE_URL="postgresql://YOUR_USERNAME:YOUR_PASSWORD@localhost:5432/brandlink?schema=public"
   ```
   
   **Don't have PostgreSQL?**
   - Install: https://www.postgresql.org/download/
   - Or use Docker: `docker run --name brandlink-db -e POSTGRES_PASSWORD=password -p 5432:5432 -d postgres`

### 2. **Install Dependencies** (if first time)
   ```bash
   npm run install:all
   ```

### 3. **Setup Database**
   ```bash
   cd backend
   npm run db:generate
   npm run db:push
   cd ..
   ```

### 4. **Start Both Servers**
   From the **root folder**, run:
   ```bash
   npm run dev
   ```
   
   You should see:
   ```
   🚀 Server running on http://localhost:3001
   ➜  Local:   http://localhost:5173/
   ```

### 5. **Open in Browser**
   Go to: **http://localhost:5173**
   
   ⚠️ **NOT** `localhost:3001` (that's just the API)

## 🔍 Troubleshooting

### Backend won't start?
- Check `backend/.env` exists and has correct `DATABASE_URL`
- Make sure PostgreSQL is running
- Check terminal for error messages

### "Cannot connect to database"?
- Verify PostgreSQL is running: `psql -U postgres`
- Check your username/password in `DATABASE_URL`
- Make sure database `brandlink` exists (or create it)

### Still seeing "ERR_CONNECTION_REFUSED"?
1. Check terminal - do you see "🚀 Server running on http://localhost:3001"?
2. If NO → Backend isn't starting (check errors above)
3. If YES → Make sure you're opening `localhost:5173` not `localhost:3001`

### Port already in use?
- Change `PORT=3002` in `backend/.env`
- Or stop whatever is using port 3001

## ✅ Success Looks Like:
- Terminal shows both servers running
- Browser opens to `localhost:5173` 
- You see the BrandLink homepage
- No Google redirect!
