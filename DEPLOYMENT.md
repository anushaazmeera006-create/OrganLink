# OrganLink Deployment Guide

## Option 1: Deploy to Render.com (Recommended - Free Tier)

### Step 1: Prepare for Deployment

1. **Create a GitHub repository**
   - Go to github.com and create a new repository
   - Upload your project files (excluding node_modules and .env)

2. **Update .env.example file**
   Create `.env.example` with placeholder values:
   ```
   DB_HOST=your-mysql-host
   DB_USER=your-mysql-user
   DB_PASSWORD=your-mysql-password
   JWT_SECRET=your-jwt-secret
   ```

### Step 2: Set up MySQL Database on Render

1. Go to [render.com](https://render.com) and sign up
2. Click "New+" → "Database" → "MySQL"
3. Choose a name (e.g., "organlink-db")
4. Select the free tier
5. Click "Create Database"
6. Wait for database to be created (takes 2-3 minutes)
7. Copy the database connection details:
   - Internal Database URL
   - Username
   - Password
   - Host
   - Port

### Step 3: Deploy Backend to Render

1. Click "New+" → "Web Service"
2. Connect your GitHub repository
3. Configure build settings:
   - **Build Command**: `npm install`
   - **Start Command**: `node server.js`
4. Add Environment Variables:
   - `DB_HOST`: Your MySQL host from Step 2
   - `DB_USER`: Your MySQL username from Step 2
   - `DB_PASSWORD`: Your MySQL password from Step 2
   - `JWT_SECRET`: Generate a random secret key
5. Click "Create Web Service"
6. Wait for deployment to complete

### Step 4: Initialize Database

1. Once deployed, go to your database dashboard on Render
2. Click "Connect" → "External Connection"
3. Use a MySQL client to run your `init.sql` file
4. Or add initialization logic to your `db.js` to run on first startup

### Step 5: Access Your Application

- Your app will be available at: `https://your-app-name.onrender.com`
- Test all functionality to ensure data loads correctly

---

## Option 2: Deploy to Railway.app (Alternative - Free Tier)

### Step 1: Install Railway CLI
```bash
npm install -g @railway/cli
```

### Step 2: Login and Initialize
```bash
railway login
railway init
```

### Step 3: Add MySQL Database
```bash
railway add mysql
```

### Step 4: Deploy
```bash
railway up
```

### Step 5: Configure Environment Variables
Railway automatically sets database environment variables. You may need to:
- Update your `db.js` to use Railway's environment variable names
- Add JWT_SECRET as an environment variable

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
