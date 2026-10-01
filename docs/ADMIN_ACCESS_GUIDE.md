# Admin Access Guide

## Problem
Cannot access `http://localhost:5173/admin` - the route requires authentication with 'admin' role.

## Solution: Create an Admin User

You have 3 options to create an admin user:

---

### Option 1: Use Python Script (Recommended)

1. Make sure your backend is running
2. Open a new terminal in the project root
3. Run:
```bash
cd backend
python create_admin.py
```

4. Follow the prompts or use defaults:
   - Email: `admin@letgo.com`
   - Password: `admin123`
   - Name: `Admin User`

---

### Option 2: Use Supabase SQL Editor

1. Go to your Supabase project dashboard
2. Click on "SQL Editor" in the left sidebar
3. Create a new query
4. Copy and paste the contents of `backend/insert_admin_user.sql`
5. Click "Run"

This creates:
- Email: `admin@letgo.com`
- Password: `admin123`

---

### Option 3: Use the Signup API with Postman/Thunder Client

1. Make sure backend is running at `http://localhost:8000`
2. Send a POST request to `http://localhost:8000/api/auth/signup`
3. Headers:
   ```
   Content-Type: application/json
   ```
4. Body (JSON):
   ```json
   {
     "full_name": "Admin User",
     "email": "admin@letgo.com",
     "password": "admin123",
     "role": "admin"
   }
   ```

---

## How to Access Admin Panel

### Step 1: Login
1. Go to `http://localhost:5173/auth`
2. Click "Login" tab
3. Enter credentials:
   - Email: `admin@letgo.com`
   - Password: `admin123`
4. Click "Login"

### Step 2: Navigate to Admin
After successful login, you can access:
- `http://localhost:5173/admin` - Admin Dashboard
- `http://localhost:5173/admin/claims` - Claims Management
- `http://localhost:5173/admin/assignments` - Field Assignments
- `http://localhost:5173/admin/broadcasts` - Broadcast Messages
- `http://localhost:5173/admin/schemes` - Schemes Management
- `http://localhost:5173/admin/reports` - Reports

---

## Troubleshooting

### "User already exists" error
The admin user is already created. Just login with:
- Email: `admin@letgo.com`
- Password: `admin123`

### Still redirected to /auth
1. Check browser console (F12) for errors
2. Verify localStorage has user data:
   ```javascript
   // In browser console:
   JSON.parse(localStorage.getItem('user'))
   ```
3. Make sure the role is 'admin' (lowercase)

### Backend not responding
1. Check if backend is running: `http://localhost:8000/docs`
2. Check `.env` file has correct Supabase credentials
3. Restart backend:
   ```bash
   cd backend
   python -m uvicorn main:app --reload --port 8000
   ```

### Database connection issues
1. Verify Supabase credentials in `backend/.env`:
   ```
   SUPABASE_URL=your_supabase_url
   SUPABASE_KEY=your_supabase_key
   ```
2. Make sure auth schema is set up (run `backend/auth/auth_schema.sql` in Supabase)

---

## Default Admin Credentials

**Email:** `admin@letgo.com`  
**Password:** `admin123`

⚠️ **IMPORTANT:** Change these credentials in production!

---

## Creating Additional Admin Users

### Via Python Script:
```bash
cd backend
python create_admin.py
```

### Via SQL:
```sql
INSERT INTO users (email, password_hash, full_name, role, is_active)
VALUES (
    'newadmin@example.com',
    '$2b$12$YOUR_BCRYPT_HASH_HERE',
    'New Admin Name',
    'admin',
    true
);
```

### Via API:
POST to `/api/auth/signup` with `"role": "admin"` in the body.

---

## User Roles

The system supports 3 roles:
- `farmer` - Regular farmer users
- `user` - General users (mapped to farmer in backend)
- `admin` - Administrator access

Admin users can access:
- All farmer/user features
- Admin panel at `/admin`
- Claims management
- Field officer assignments
- Broadcast messaging
- Reports and analytics
