# Pro Assignment 4: Production Deployment

## Learning Objectives

By completing this assignment, you will:
- Understand the process of deploying applications to production
- Learn to configure environment variables for production
- Practice setting up production-ready configurations
- Gain experience with deployment platforms (Vercel, Railway, Heroku, etc.)
- Understand the difference between development and production environments
- Learn to troubleshoot deployment issues

---

## Prerequisites

- Completed at least Assignment 2 (E2E Hello World)
- Working server and client application
- Understanding of your chosen stack (Node.js or Python)
- Cursor AI installed and configured
- GitHub account with repository access
- Account on a deployment platform (free tier is sufficient)

---

## Overview

This is a **pro-level bonus assignment** worth **10 bonus points**. It's optional but highly recommended for students who want to learn professional deployment practices.

**Goal:** Deploy your application to a production environment so it's accessible on the internet.

---

## Instructions

### Step 1: Choose Your Deployment Platform

Select a deployment platform based on your stack and preferences:

**Recommended Platforms:**

**For Node.js:**
- **Vercel** (recommended) - Easy, free, great for Node.js
- **Railway** - Simple, free tier, good for full-stack apps
- **Render** - Free tier, easy setup
- **Heroku** - Classic, but limited free tier

**For Python:**
- **Railway** (recommended) - Great for Python apps
- **Render** - Good Python support, free tier
- **Heroku** - Classic, but limited free tier
- **Fly.io** - Modern, good free tier

**For Static + API:**
- **Vercel** - Best for static sites with API routes
- **Netlify** - Great for static sites
- **Railway** - Good for full-stack apps

### Step 2: Prepare Your Application

1. **Ensure your app works locally:**
   ```bash
   # Node.js
   npm start
   # Test at http://localhost:3000

   # Python
   python server/app.py
   # Test at http://localhost:5000
   ```

2. **Create production-ready configuration:**

   **Node.js (package.json):**
   ```json
   {
     "scripts": {
       "start": "node server/index.js",
       "dev": "node server/index.js"
     },
     "engines": {
       "node": ">=18.0.0"
     }
   }
   ```

   **Python (requirements.txt):**
   ```txt
   flask==3.0.0
   # or express equivalent
   ```

3. **Add .gitignore (if not present):**
   ```
   node_modules/
   .env
   .env.local
   __pycache__/
   *.pyc
   .venv/
   ```

### Step 3: Set Up Environment Variables

1. **Identify environment variables:**
   - Port (usually set automatically by platform)
   - API URLs (if needed)
   - Any configuration values

2. **Use environment variables in code:**

   **Node.js:**
   ```javascript
   const PORT = process.env.PORT || 3000;
   const API_URL = process.env.API_URL || 'http://localhost:3000';
   ```

   **Python:**
   ```python
   import os
   PORT = int(os.environ.get('PORT', 5000))
   API_URL = os.environ.get('API_URL', 'http://localhost:5000')
   ```

### Step 4: Deploy to Platform

#### Option A: Deploy to Vercel (Node.js recommended)

1. **Install Vercel CLI:**
   ```bash
   npm install -g vercel
   ```

2. **Login:**
   ```bash
   vercel login
   ```

3. **Deploy:**
   ```bash
   vercel
   ```

4. **Follow prompts:**
   - Link to existing project or create new
   - Configure settings
   - Deploy!

5. **Set environment variables (if needed):**
   - Go to Vercel dashboard → Project → Settings → Environment Variables
   - Add any required variables

#### Option B: Deploy to Railway (Node.js or Python)

1. **Sign up:** Go to [railway.app](https://railway.app)

2. **Create new project:**
   - Click "New Project"
   - Select "Deploy from GitHub repo"
   - Choose your repository

3. **Configure:**
   - Railway auto-detects your stack
   - Set start command if needed:
     - Node.js: `npm start`
     - Python: `python server/app.py`

4. **Set environment variables:**
   - Go to Variables tab
   - Add any required variables

5. **Deploy:**
   - Railway automatically deploys on push
   - Or click "Deploy" button

#### Option C: Deploy to Render (Node.js or Python)

1. **Sign up:** Go to [render.com](https://render.com)

2. **Create new service:**
   - Click "New +" → "Web Service"
   - Connect GitHub repository

3. **Configure:**
   - **Name:** Your app name
   - **Environment:** Node or Python
   - **Build Command:** `npm install` (Node) or `pip install -r requirements.txt` (Python)
   - **Start Command:** `npm start` (Node) or `python server/app.py` (Python)

4. **Set environment variables:**
   - Go to Environment tab
   - Add variables

5. **Deploy:**
   - Click "Create Web Service"
   - Render builds and deploys automatically

### Step 5: Test Your Deployed Application

1. **Get your deployment URL:**
   - Vercel: `https://your-app.vercel.app`
   - Railway: `https://your-app.railway.app`
   - Render: `https://your-app.onrender.com`

2. **Test the application:**
   - Open URL in browser
   - Test all endpoints
   - Verify client works
   - Check for errors

3. **Test API endpoint:**
   ```bash
   curl https://your-app.vercel.app/api/hello
   # Should return: {"message":"Hello Vibe!"}
   ```

### Step 6: Handle CORS (if needed)

If your client and server are on different domains, configure CORS:

**Node.js:**
```javascript
// Allow your deployment URL
app.use((req, res, next) => {
  const allowedOrigins = [
    'https://your-app.vercel.app',
    'http://localhost:3000'
  ];
  const origin = req.headers.origin;
  if (allowedOrigins.includes(origin)) {
    res.header('Access-Control-Allow-Origin', origin);
  }
  res.header('Access-Control-Allow-Headers', 'Content-Type');
  next();
});
```

**Python:**
```python
from flask_cors import CORS

app = Flask(__name__)
CORS(app, origins=[
    'https://your-app.vercel.app',
    'http://localhost:5000'
])
```

### Step 7: Update Client to Use Production URL

1. **Update client code to use production API:**

   **If client is on same domain:**
   - Use relative URLs: `/api/hello`

   **If client is on different domain:**
   - Update fetch URL: `https://your-api.railway.app/api/hello`

2. **Test client with production API:**
   - Open client URL
   - Verify it fetches from production API
   - Check browser console for errors

### Step 8: Document Your Deployment

1. **Update README.md:**
   - Add "Deployment" section
   - Include deployment URL
   - Document environment variables
   - Add deployment instructions
   - Include troubleshooting tips

2. **Screenshot:**
   - Take screenshot of deployed application
   - Include in README.md

---

## Requirements

### Required

- [ ] Application deployed to production platform
- [ ] Live URL accessible and working
- [ ] Environment variables configured (if needed)
- [ ] Client can access production API
- [ ] Application works in production environment
- [ ] Deployment documented in README.md

### Optional

- [ ] Custom domain configured
- [ ] HTTPS enabled (usually automatic)
- [ ] CI/CD pipeline set up (auto-deploy on push)
- [ ] Monitoring/logging configured

---

## Acceptance Criteria

Your submission will be evaluated based on:

- [ ] Application successfully deployed to production
- [ ] Live URL is accessible
- [ ] All endpoints work in production
- [ ] Client can access production API
- [ ] Environment variables properly configured
- [ ] Deployment documented in README.md
- [ ] Screenshot of deployed application included
- [ ] No critical errors in production
- [ ] Changes committed and pushed to GitHub

---

## Submission Requirements

1. **Live URL:** Share your production URL
2. **Documentation:** README.md updated with deployment section
3. **Screenshot:** Screenshot of deployed application
4. **Commit:** All changes committed and pushed to GitHub

**Commit message example:**
```bash
git commit -m "Pro Assignment 4: Production Deployment"
```

---

## Grading Rubric

See [Grading Rubrics](../materials/grading-rubrics.md) for detailed criteria.

**Total Points:** 10 bonus points

- **Deployment success:** 4 points
  - Application deployed and accessible: 2 points
  - All endpoints working: 2 points
- **Configuration:** 3 points
  - Environment variables configured: 1 point
  - Production-ready configuration: 1 point
  - CORS handled (if needed): 1 point
- **Documentation:** 2 points
  - Deployment documented: 1 point
  - Screenshot included: 1 point
- **Code quality:** 1 point
  - Production-ready code
  - No hardcoded localhost URLs

---

## Tips for Success

- **Start with free tier:** All platforms offer free tiers sufficient for this assignment
- **Use Cursor AI:** Ask Cursor to help with deployment configuration
- **Test locally first:** Make sure everything works locally before deploying
- **Check platform logs:** If deployment fails, check platform logs for errors
- **Read platform docs:** Each platform has excellent documentation
- **Start simple:** Deploy basic version first, then add features
- **Handle errors gracefully:** Production apps should handle errors well

---

## Common Deployment Issues

### Issue: Application won't start

**Solutions:**
- Check start command in platform settings
- Verify PORT environment variable is used
- Check platform logs for errors
- Ensure all dependencies are in package.json/requirements.txt

### Issue: CORS errors

**Solutions:**
- Configure CORS to allow your client domain
- Check allowed origins in CORS configuration
- Verify client is using correct API URL

### Issue: Environment variables not working

**Solutions:**
- Verify variables are set in platform dashboard
- Check variable names match code
- Restart deployment after adding variables

### Issue: Build fails

**Solutions:**
- Check build logs for errors
- Verify all dependencies are listed
- Check Node.js/Python version compatibility
- Ensure build command is correct

---

## Example Deployment Structure

```
your-project/
├── server/
│   └── index.js (or app.py)
├── client/
│   └── index.html
├── package.json (or requirements.txt)
├── .gitignore
├── vercel.json (optional, for Vercel)
├── Procfile (optional, for Heroku)
└── README.md
```

**Example vercel.json (Vercel):**
```json
{
  "version": 2,
  "builds": [
    {
      "src": "server/index.js",
      "use": "@vercel/node"
    }
  ],
  "routes": [
    {
      "src": "/api/(.*)",
      "dest": "server/index.js"
    }
  ]
}
```

**Example Procfile (Heroku):**
```
web: node server/index.js
```

---

## Getting Help

- Ask questions in the help channel
- Review platform documentation:
  - [Vercel Documentation](https://vercel.com/docs)
  - [Railway Documentation](https://docs.railway.app/)
  - [Render Documentation](https://render.com/docs)
- Check [FAQ](../materials/faq.md)
- Review [Student Guide](../materials/student-guide.md)
- Contact your teacher if needed

---

## Resources

**Deployment Platforms:**
- [Vercel](https://vercel.com/) - Best for Node.js and static sites
- [Railway](https://railway.app/) - Great for full-stack apps
- [Render](https://render.com/) - Good for Node.js and Python
- [Heroku](https://www.heroku.com/) - Classic platform

**Deployment Guides:**
- [Deploying Node.js Apps](https://vercel.com/docs/deployments/overview)
- [Deploying Python Apps](https://docs.railway.app/guides/python)
- [Environment Variables Guide](https://vercel.com/docs/environment-variables)

---

## Document History

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2025-12-25 | RepodIn Education Team | Initial version |

---

**Next Review Date:** 2026-03-20

