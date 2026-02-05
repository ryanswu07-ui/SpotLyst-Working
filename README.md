# BrandLink Marketplace

A two-sided marketplace connecting brands with influencers. Brands can discover creators, see verified past collaborations with proof, and contact or book them without DMs or agents.

## Features (MVP)

### Influencer Features
- Public profile with platforms, follower counts, and niche tags
- Past collaborations showcase with proof media
- Rate card with pricing for standard deliverables
- Link-in-bio URL (username.brandlink.com)
- Receive structured deal proposals

### Brand Features
- Search and filter influencers by platform, category, follower count
- View influencer profiles with past collaborations and proof
- Send structured deal proposals
- In-platform messaging for negotiations

### Admin Features
- User management and moderation
- Report handling
- Basic analytics dashboard

## Tech Stack

- **Backend**: Node.js + Express + TypeScript
- **Database**: PostgreSQL with Prisma ORM
- **Frontend**: React + TypeScript + Vite
- **Authentication**: JWT + Google OAuth

## Getting Started

### Prerequisites

- Node.js 18+ and npm
- PostgreSQL database
- Google OAuth credentials (for social login)

### Installation

1. Clone the repository
2. Install dependencies:
   ```bash
   npm run install:all
   ```

3. Set up environment variables:
   - Copy `backend/.env.example` to `backend/.env`
   - Fill in your database URL, JWT secret, and Google OAuth credentials

4. Set up the database:
   ```bash
   cd backend
   npm run db:generate
   npm run db:push
   ```

5. Start development servers:
   ```bash
   npm run dev
   ```

   This will start:
   - Backend API on http://localhost:3001
   - Frontend on http://localhost:5173

## Project Structure

```
.
├── backend/          # Express API server
│   ├── src/
│   │   ├── routes/   # API routes
│   │   ├── middleware/
│   │   └── server.ts
│   ├── prisma/       # Database schema
│   └── package.json
├── frontend/         # React application
└── package.json      # Root workspace config
```

## API Endpoints

### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login
- `GET /api/auth/google` - Google OAuth
- `GET /api/auth/me` - Get current user

### Influencer
- `GET /api/influencer/profile/:username` - Public profile
- `GET /api/influencer/my-profile` - Own profile
- `POST /api/influencer/profile` - Create/update profile
- `POST /api/influencer/platforms` - Update platform stats
- `POST /api/influencer/collaborations` - Add past collaboration
- `POST /api/influencer/rate-card` - Update rate card

### Brand
- `GET /api/brand/search` - Search influencers
- `POST /api/brand/profile` - Create/update brand profile

### Proposals
- `POST /api/proposals` - Create proposal
- `GET /api/proposals` - List proposals
- `GET /api/proposals/:id` - Get proposal details
- `PATCH /api/proposals/:id/status` - Update status

### Messages
- `POST /api/messages` - Send message
- `GET /api/messages/proposal/:id` - Get messages

### Admin
- `GET /api/admin/users` - List users
- `GET /api/admin/reports` - List reports
- `GET /api/admin/analytics` - Analytics dashboard

## Development

### Backend
```bash
cd backend
npm run dev        # Start dev server
npm run db:studio  # Open Prisma Studio
```

### Frontend
```bash
cd frontend
npm run dev        # Start dev server
npm run build      # Build for production
```

## License

MIT
