# Google OAuth Setup Instructions

Google OAuth is currently **commented out** in the Login and Register pages to prevent the blank page issue.

## How to Enable Google OAuth

### 1. Get Google OAuth Credentials

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project or select an existing one
3. Enable the **Google+ API** (or Google People API)
4. Go to **Credentials** → **Create Credentials** → **OAuth 2.0 Client ID**
5. Configure OAuth consent screen:
   - Application name: BrandLink
   - User support email: your email
   - Authorized domains: localhost (for development)
6. Create OAuth Client ID:
   - Application type: **Web application**
   - Name: BrandLink Web
   - Authorized JavaScript origins:
     - `http://localhost:5173`
     - `http://localhost:3001`
   - Authorized redirect URIs:
     - `http://localhost:3001/api/auth/google/callback`

### 2. Configure Backend

Edit `backend/.env` and add:

```env
GOOGLE_CLIENT_ID=your-actual-client-id-from-google
GOOGLE_CLIENT_SECRET=your-actual-client-secret-from-google
GOOGLE_CALLBACK_URL=http://localhost:3001/api/auth/google/callback
```

### 3. Configure Frontend (Optional)

Create `frontend/.env.local`:

```env
VITE_GOOGLE_CLIENT_ID=your-actual-client-id-from-google
```

### 4. Uncomment OAuth Buttons

In `frontend/src/pages/Login.tsx` and `frontend/src/pages/Register.tsx`, uncomment the Google OAuth section:

```tsx
<div className="auth-divider">
  <span>OR</span>
</div>

<button onClick={handleGoogleLogin} className="btn btn-secondary" style={{ width: '100%' }}>
  Continue with Google
</button>
```

### 5. Restart Servers

```bash
npm run dev
```

## Testing OAuth

1. Click "Continue with Google"
2. You'll be redirected to Google sign-in
3. After authentication, you'll be redirected to `/auth/callback`
4. The callback page will extract the token and redirect to your dashboard

## Current Workaround

For now, use **email/password authentication**:
- Register with email, password, and choose your role
- Login with email and password

Google OAuth can be enabled later when you have production credentials.
