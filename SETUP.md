# BrandLink Marketplace - Setup Guide

## Quick Start

### 1. Install Dependencies

```bash
npm run install:all
```

This installs dependencies for both backend and frontend.

### 2. Database Setup

1. **Install PostgreSQL** (if not already installed)
   - Download from https://www.postgresql.org/download/
   - Or use Docker: `docker run --name brandlink-db -e POSTGRES_PASSWORD=password -p 5432:5432 -d postgres`

2. **Configure Database**
   - Copy `backend/.env.example` to `backend/.env`
   - Update `DATABASE_URL` with your PostgreSQL connection string:
     ```
     DATABASE_URL="postgresql://username:password@localhost:5432/brandlink?schema=public"
     ```

3. **Initialize Database**
   ```bash
   cd backend
   npm run db:generate  # Generate Prisma client
   npm run db:push      # Create database schema
   ```

### 3. Environment Variables

Edit `backend/.env` and set:

- `DATABASE_URL` - Your PostgreSQL connection string
- `JWT_SECRET` - A random secret string for JWT tokens
- `GOOGLE_CLIENT_ID` - (Optional) For Google OAuth
- `GOOGLE_CLIENT_SECRET` - (Optional) For Google OAuth
- `GOOGLE_CALLBACK_URL` - (Optional) Usually `http://localhost:3001/api/auth/google/callback`
- `FRONTEND_URL` - Usually `http://localhost:5173`

### 4. Start Development Servers

From the root directory:

```bash
npm run dev
```

This starts:
- Backend API on http://localhost:3001
- Frontend on http://localhost:5173

### 5. Create Your First Admin User

You can create an admin user directly in the database or via a script. For MVP, you can manually update a user's role in the database:

```sql
UPDATE "User" SET role = 'ADMIN' WHERE email = 'your-email@example.com';
```

## Project Structure

```
.
├── backend/
│   ├── src/
│   │   ├── routes/        # API route handlers
│   │   ├── middleware/    # Auth, error handling
│   │   └── server.ts      # Express app entry point
│   ├── prisma/
│   │   └── schema.prisma  # Database schema
│   └── package.json
├── frontend/
│   ├── src/
│   │   ├── components/    # React components
│   │   ├── pages/         # Page components
│   │   ├── store/         # Zustand state management
│   │   ├── services/      # API client
│   │   └── App.tsx        # Main app component
│   └── package.json
└── package.json           # Workspace root
```

## Key Features Implemented

✅ **Authentication**
- Email/password registration and login
- Google OAuth (configured, needs credentials)
- JWT-based session management
- Role-based access control (Influencer, Brand, Admin)

✅ **Influencer Features**
- Profile creation with platforms and stats
- Past collaborations with proof media
- Rate card management
- Public profile pages (`/@username`)
- Link-in-bio URL generation

✅ **Brand Features**
- Brand profile creation
- Influencer search with filters (platform, category, followers)
- View influencer profiles
- Send structured proposals

✅ **Proposals & Messaging**
- Create proposals with deliverables, budget, timeline
- Proposal status tracking (NEW, IN_DISCUSSION, DECLINED, CLOSED)
- Threaded messaging per proposal
- Mark deals as closed

✅ **Admin Panel**
- User management
- Report handling
- Analytics dashboard

## Next Steps

1. **Add Profile Editing Pages**: Create forms for editing influencer and brand profiles
2. **Add Proposal Creation Form**: Build the UI for brands to create proposals from influencer profiles
3. **Add Collaboration Management**: UI for influencers to add/edit past collaborations
4. **Add Rate Card Editor**: UI for managing rate card items
5. **File Upload**: Implement image/video upload for proof media (currently links only)
6. **Email Notifications**: Send emails when proposals are received
7. **Enhanced Search**: Add more filters and sorting options

## Testing

To test the application:

1. Register as an Influencer
2. Create a profile with platforms and stats
3. Add past collaborations
4. Set up a rate card
5. Register as a Brand (use different email)
6. Search for the influencer
7. Send a proposal
8. Log in as the influencer and respond

## Troubleshooting

**Database connection errors:**
- Ensure PostgreSQL is running
- Check DATABASE_URL in `.env`
- Run `npm run db:push` again

**Port already in use:**
- Change PORT in `backend/.env`
- Update FRONTEND_URL proxy in `frontend/vite.config.ts`

**CORS errors:**
- Ensure FRONTEND_URL in backend `.env` matches your frontend URL
- Check that both servers are running

**Google OAuth not working:**
- Ensure GOOGLE_CLIENT_ID and GOOGLE_CLIENT_SECRET are set
- Add `http://localhost:3001/api/auth/google/callback` to Google OAuth redirect URIs
- Add `http://localhost:5173` to authorized JavaScript origins

## Production Deployment

For production:

1. Set `NODE_ENV=production`
2. Use a production database (e.g., AWS RDS, Heroku Postgres)
3. Set secure JWT_SECRET
4. Configure CORS for your production domain
5. Build frontend: `npm run build:frontend`
6. Serve frontend static files or deploy to Vercel/Netlify
7. Deploy backend to Heroku, Railway, or AWS
