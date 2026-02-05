# Database Setup Guide

## The Problem
You're seeing: `Can't reach database server at localhost:5432`

This means PostgreSQL (the database) isn't running or isn't configured correctly.

## Option 1: Install PostgreSQL (Recommended)

### Step 1: Download PostgreSQL
1. Go to: https://www.postgresql.org/download/windows/
2. Download the Windows installer
3. Run the installer

### Step 2: Install PostgreSQL
1. Click "Next" through the installation wizard
2. **Important:** Remember the password you set for the `postgres` user!
3. Port: Keep default `5432`
4. Complete the installation

### Step 3: Create Database
1. Open **pgAdmin** (comes with PostgreSQL) or use **Command Prompt**
2. In Command Prompt, run:
   ```bash
   psql -U postgres
   ```
   (Enter your password when prompted)

3. Create the database:
   ```sql
   CREATE DATABASE brandlink;
   ```
4. Exit: `\q`

### Step 4: Update .env File
Edit `backend/.env` and update the `DATABASE_URL`:
```env
DATABASE_URL="postgresql://postgres:YOUR_PASSWORD@localhost:5432/brandlink?schema=public"
```
Replace `YOUR_PASSWORD` with the password you set during installation.

### Step 5: Run Database Migrations
```bash
cd backend
npm run db:generate
npm run db:push
```

## Option 2: Use Docker (Easier)

If you have Docker installed:

1. Run PostgreSQL in Docker:
   ```bash
   docker run --name brandlink-db -e POSTGRES_PASSWORD=password -p 5432:5432 -d postgres
   ```

2. Update `backend/.env`:
   ```env
   DATABASE_URL="postgresql://postgres:password@localhost:5432/postgres?schema=public"
   ```

3. Create the database:
   ```bash
   docker exec -it brandlink-db psql -U postgres -c "CREATE DATABASE brandlink;"
   ```

4. Update `backend/.env` again:
   ```env
   DATABASE_URL="postgresql://postgres:password@localhost:5432/brandlink?schema=public"
   ```

5. Run migrations:
   ```bash
   cd backend
   npm run db:generate
   npm run db:push
   ```

## Option 3: Use SQLite (Simplest for Development)

If you want to avoid PostgreSQL setup, we can switch to SQLite. Let me know if you want this option.

## Verify Database Connection

After setting up, test the connection:
```bash
cd backend
npm run db:push
```

If you see "Database schema is up to date", it's working!

## Troubleshooting

### "psql: command not found"
- Add PostgreSQL to your PATH, or use pgAdmin instead

### "Password authentication failed"
- Check your password in `backend/.env`
- Try resetting PostgreSQL password

### "Port 5432 already in use"
- Another PostgreSQL instance is running
- Stop it or use a different port

### Still having issues?
Share the error message and I'll help troubleshoot!
