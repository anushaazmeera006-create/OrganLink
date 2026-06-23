# OrganLink Deployment Guide

## Deploy to Glitch + PlanetScale (Free & Long-term)

### STEP 1: Set up PlanetScale MySQL Database

1. Go to [planetscale.com](https://planetscale.com) and sign up (free)
2. Click "New Database" 
3. Name it: `organlink`
4. Select region closest to you
5. Click "Create Database"
6. Wait 1-2 minutes for database to be created
7. Click on your database
8. Go to "Connect" → "General" → "Connect with"
9. Select "Node.js" and copy these credentials:
   - **Host** (e.g., `aws.connect.psdb.cloud`)
   - **Username**
   - **Password**
   - **Database name** (usually same as database name)

### STEP 2: Run Database Schema on PlanetScale

1. In PlanetScale, click "Console" or "SQL Editor"
2. Copy the contents of your `init.sql` file
3. Paste it into the SQL editor
4. Click "Run" to create all tables
5. This will create: users, person, donor, recipient, organ, hospital tables

### STEP 3: Create Glitch Project

1. Go to [glitch.com](https://glitch.com) and sign up/login
2. Click "New Project" → "Import from GitHub"
3. Authorize Glitch to access your GitHub
4. Select your repository: `anushaazmeera006-create/OrganLink`
5. Click "Import"
6. Wait for Glitch to import your project

### STEP 4: Configure Environment Variables in Glitch

1. In Glitch, click the project name (top left)
2. Click ".env" file (or create it if doesn't exist)
3. Add these variables with your PlanetScale credentials:
   ```
   DB_HOST=your-planetscale-host
   DB_USER=your-planetscale-username
   DB_PASSWORD=your-planetscale-password
   DB_NAME=organlink
   DB_PORT=3306
   JWT_SECRET=organlink_secret_key_2024
   ```
4. Replace the values with your actual PlanetScale credentials from Step 1

### STEP 5: Start the Application

1. In Glitch, click "Logs" (bottom panel)
2. Click "Start" or "Refresh" to restart the server
3. Wait for it to show "Server running on..."
4. Click "Show" (top button) to open your live app
5. Your app URL will be: `https://your-project-name.glitch.me`

### STEP 6: Test Your Application

1. Open your Glitch app URL
2. Check if dashboard loads with data
3. Test adding donors, recipients
4. Test the matching algorithm
5. Verify all features work

### IMPORTANT NOTES:

- **Your Glitch link will stay active as long as your project is active**
- **PlanetScale database is free and permanent**
- **Both services are completely free**
- **No migration needed - stays on MySQL**
- **Links are stable for long-term use**

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
