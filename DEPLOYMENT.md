# OrganLink Deployment Guide

## Deploy to Railway.app (Recommended - Free Tier)

### Step 1: Sign up for Railway

1. Go to [railway.app](https://railway.app) and sign up/login
2. Click "New Project" or "Start a New Project"

### Step 2: Connect GitHub Repository

1. Click "Deploy from GitHub repo"
2. Authorize Railway to access your GitHub account
3. Select your repository: `anushaazmeera006-create/OrganLink`
4. Click "Import"

### Step 3: Add MySQL Database

1. In your Railway project, click "New Service"
2. Select "Database" → "MySQL"
3. Railway will automatically create a MySQL database
4. Wait for the database to be provisioned (takes 1-2 minutes)

### Step 4: Configure Environment Variables

Railway automatically sets database environment variables. You need to:

1. Click on your web service (the one from your GitHub repo)
2. Go to "Variables" tab
3. Add these environment variables:
   - `DB_HOST`: `${{MYSQLHOST}}`
   - `DB_USER`: `${{MYSQLUSER}}`
   - `DB_PASSWORD`: `${{MYSQLPASSWORD}}`
   - `DB_NAME`: `${{MYSQLDATABASE}}`
   - `DB_PORT`: `${{MYSQLPORT}}`
   - `JWT_SECRET`: Generate a random secret (e.g., `organlink_secret_key_2024`)

### Step 5: Update db.js for Railway Environment Variables

Update your `db.js` to use Railway's environment variable names:

---

## Important Notes

### Database Initialization
Your `init.sql` file needs to be executed on the cloud database. Options:
1. Use a MySQL client to connect and run the SQL file
2. Add initialization code to `db.js` that runs on first startup
3. Use the database provider's web console to run SQL

### Environment Variables
Never commit your `.env` file to GitHub. Use the platform's environment variable management instead.

### Troubleshooting
- If data doesn't load, check the database connection in the logs
- Ensure CORS is properly configured for your production domain
- Verify all API routes are accessible without authentication
- Check that the database schema matches your queries

### Performance Considerations
- Free tiers may have limitations on database connections
- Consider implementing connection pooling for better performance
- Add error handling for database timeouts
