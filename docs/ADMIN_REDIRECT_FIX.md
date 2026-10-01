# Admin Redirect Fix

## Issue
When navigating to `/admin`, users are being redirected to `/dashboard` even when logged in as admin.

## Changes Made

### 1. Added Debug Page
Created `/debug-auth` route to help diagnose authentication issues:
- Shows raw localStorage data
- Displays parsed user object
- Shows user role
- Provides quick actions (clear storage, refresh, try /admin)

**Usage:** Navigate to `http://localhost:5173/debug-auth` after logging in

### 2. Enhanced ProtectedRoute Logging
Added console.log statements to ProtectedRoute to help debug:
- Logs current user role
- Logs allowed roles
- Logs access decisions

### 3. Fixed Admin Index Route
Changed `/admin` index route to explicitly redirect to `/admin/dashboard`

## How to Test

### Step 1: Check Your Current Login
1. Navigate to `http://localhost:5173/debug-auth`
2. Check the "Role" field - it should say "admin"
3. If it says "farmer" or "user", you're not logged in as admin

### Step 2: Login as Admin
If you don't have an admin account:
1. Run `create_admin.bat` or `cd backend && python create_admin.py`
2. Go to `http://localhost:5173/auth`
3. Login with:
   - Email: `admin@letgo.com`
   - Password: `admin123`

### Step 3: Verify Admin Access
1. After login, you should be automatically redirected to `/admin`
2. If not, manually navigate to `http://localhost:5173/admin`
3. You should see the admin dashboard

### Step 4: Check Browser Console
Open browser console (F12) and look for ProtectedRoute logs:
```
ProtectedRoute - User Role: admin Allowed Roles: ['admin']
Access granted
```

## Common Issues

### Issue: Role is "farmer" or "user" instead of "admin"
**Solution:** You're not logged in as admin. Create an admin user and login again.

### Issue: Role is undefined or null
**Solution:** 
1. Clear localStorage: `localStorage.clear()`
2. Login again
3. Check if backend is returning user data correctly

### Issue: Still redirected after confirming role is "admin"
**Solution:**
1. Check browser console for errors
2. Verify ProtectedRoute logs show "Access granted"
3. Clear browser cache and try again
4. Check if there's a typo in the role (e.g., "Admin" vs "admin")

### Issue: Backend returns role as "Admin" (capitalized)
**Solution:** The ProtectedRoute normalizes roles to lowercase, so this should work. But verify in `/debug-auth`.

## Files Modified
- `frontend/src/components/ProtectedRoute.jsx` - Added logging
- `frontend/src/App.jsx` - Fixed admin index route, added debug route
- `frontend/src/pages/DebugAuth.jsx` - New debug page

## Next Steps
1. Visit `/debug-auth` to see your current auth state
2. If role is not "admin", create admin user and login
3. If role is "admin" but still redirected, check browser console logs
4. Report any console errors for further debugging
