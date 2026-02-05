# 🚀 How to Start the App

## The Problem
You're seeing "ERR_CONNECTION_REFUSED" because **the backend server isn't running**.

## Quick Fix Steps:

### Step 1: Create Backend Environment File

Create a file called `.env` in the `backend` folder with this content:

```env
# Server
PORT=3001
NODE_ENV=development

# Database (UPDATE THIS WITH YOUR POSTGRESQL CONNECTION)
DATABASE_URL="postgresql://postgres:password@localhost:5432/brandlink?schema=public"

# JWT Secret (CHANGE THIS TO A RANDOM STRING)
JWT_SECRET=your-super-secret-jwt-key-change-in-production-12345
JWT_EXPIRES_IN=7d

# Frontend URL
FRONTEND_URL=http://localhost:5173

# Google OAuth (LEAVE EMPTY - we disabled it)
# GOOGLE_CLIENT_ID=
# GOOGLE_CLIENT_SECRET=
# GOOGLE_CALLBACK_URL=
```

**Important:** Update `DATABASE_URL` with your actual PostgreSQL username and password!

### Step 2: Install Dependencies (if not done)

```bash
npm run install:all
```

### Step 3: Setup Database

```bash
cd backend
npm run db:generate
npm run db:push
cd ..
```

**Note:** Make sure PostgreSQL is running! If you don't have PostgreSQL:
- Install it from https://www.postgresql.org/download/
- Or use Docker: `docker run --name brandlink-db -e POSTGRES_PASSWORD=password -p 5432:5432 -d postgres`

### Step 4: Start the Servers

From the **root folder** (not backend or frontend):

```bash
npm run dev
```

You should see:
```
🚀 Server running on http://localhost:3001
VITE v5.x.x  ready in xxx ms
➜  Local:   http://localhost:5173/
```

### Step 5: Open the App

Open your browser to:
```
http://localhost:5173
```

**NOT** `localhost:3001` (that's just the API)

## Troubleshooting

### "Cannot connect to database"
- Make sure PostgreSQL is running
- Check your `DATABASE_URL` in `backend/.env`
- Try: `psql -U postgres` to test database connection

### "Port 3001 already in use"
- Another app is using port 3001
- Change `PORT=3002` in `backend/.env` (and update `FRONTEND_URL` proxy if needed)

### "Module not found" errors
- Run `npm run install:all` again
- Make sure you're in the root folder

### Still seeing "ERR_CONNECTION_REFUSED"?
1. Check terminal - is the backend server actually starting?
2. Look for error messages in the terminal
3. Make sure you're opening `localhost:5173` not `localhost:3001`

## What Should Happen

When you run `npm run dev`, you should see TWO servers start:
1. ✅ Backend on port 3001
2. ✅ Frontend on port 5173

Then open `http://localhost:5173` in your browser!
