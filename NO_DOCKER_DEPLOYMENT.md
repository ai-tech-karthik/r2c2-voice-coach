# 🚀 No-Docker Deployment Guide

If you don't want to install Docker or need a faster deployment, here are alternatives:

## Option 1: Deploy to Render.com (No Docker Needed) ⭐ RECOMMENDED

Render.com builds Docker images for you in the cloud!

### Step 1: Push to GitHub (5 minutes)

```bash
cd r2c2-voice-coach

# Initialize git if not already done
git init
git add .
git commit -m "Initial commit - R2C2 Voice Coach"

# Create a new repository on GitHub, then:
git remote add origin https://github.com/YOUR_USERNAME/r2c2-voice-coach.git
git push -u origin main
```

### Step 2: Deploy Backend to Render (5 minutes)

1. Go to https://render.com and sign up (free)
2. Click "New +" → "Web Service"
3. Connect your GitHub repository
4. Configure:
   - **Name**: `r2c2-voice-coach`
   - **Region**: Choose closest to you
   - **Branch**: `main`
   - **Root Directory**: `server`
   - **Runtime**: `Docker`
   - **Docker Command**: Leave empty (uses Dockerfile)

5. Add Environment Variables:
   ```
   DAILY_API_KEY=e5dd8a809058d2d681563ac4d58f242bc03ceeb91cf25ee776b772d5b43d0aac
   GOOGLE_API_KEY=AIzaSyAY3H_bhXWnydY23P_uiSvOcMOzSZ5-GYk
   DATABASE_PATH=./data/r2c2_coach.db
   API_PORT=7860
   API_HOST=0.0.0.0
   ```

6. Click "Create Web Service"

7. Wait for deployment (5-10 minutes)

8. Copy your Render URL: `https://r2c2-voice-coach.onrender.com`

### Step 3: Deploy Frontend to Vercel (5 minutes)

```bash
cd client

# Update .env.local with Render URL
cat > .env.local << EOF
BOT_START_URL="https://r2c2-voice-coach.onrender.com/start"
BOT_START_PUBLIC_API_KEY=""
NEXT_PUBLIC_API_BASE_URL="https://r2c2-voice-coach.onrender.com"
NEXT_PUBLIC_ENABLE_EMOTION_VIZ=true
NEXT_PUBLIC_ENABLE_PLAN_EDITING=true
NEXT_PUBLIC_DEBUG_MODE=false
EOF

# Deploy
npm install -g vercel
vercel login
vercel --prod
```

**Done!** Your app is live.

---

## Option 2: Railway.app (Also No Docker Needed)

### Step 1: Push to GitHub (same as above)

### Step 2: Deploy to Railway

1. Go to https://railway.app and sign up
2. Click "New Project" → "Deploy from GitHub repo"
3. Select your repository
4. Railway auto-detects the Dockerfile and builds it
5. Add environment variables in Railway dashboard
6. Deploy!

---

## Option 3: Local Development + Ngrok (Fastest - 5 minutes)

Perfect for quick demos!

### Step 1: Start Backend Locally

```bash
cd r2c2-voice-coach/server

# Make sure .env is configured
uv sync
uv run bot.py --transport daily
```

### Step 2: Expose with Ngrok

```bash
# Install ngrok
brew install ngrok

# Or download from https://ngrok.com/download

# Expose port 7860
ngrok http 7860
```

Copy the ngrok URL (e.g., `https://abc123.ngrok.io`)

### Step 3: Deploy Frontend

```bash
cd ../client

# Update .env.local with ngrok URL
cat > .env.local << EOF
BOT_START_URL="https://abc123.ngrok.io/start"
BOT_START_PUBLIC_API_KEY=""
NEXT_PUBLIC_API_BASE_URL="https://abc123.ngrok.io"
NEXT_PUBLIC_ENABLE_EMOTION_VIZ=true
NEXT_PUBLIC_ENABLE_PLAN_EDITING=true
NEXT_PUBLIC_DEBUG_MODE=false
EOF

# Deploy to Vercel
vercel --prod
```

**Pros**: Fastest setup (5 minutes total)
**Cons**: Ngrok URL changes on restart, computer must stay on

---

## Comparison

| Method | Time | Docker Needed | Cost | Best For |
|--------|------|---------------|------|----------|
| Render.com | 15 min | No (cloud builds) | Free | Hackathons |
| Railway.app | 15 min | No (cloud builds) | $5 credit | Quick demos |
| Ngrok + Local | 5 min | No | Free | Testing |
| Pipecat Cloud | 20 min | Yes | Varies | Production |

---

## Recommended: Render.com

For your hackathon, I recommend **Render.com** because:
- ✅ No Docker installation needed
- ✅ Free tier available
- ✅ Builds Docker in the cloud
- ✅ Easy to set up
- ✅ Reliable for demos
- ✅ Auto-deploys on git push

---

## Quick Start with Render.com

```bash
# 1. Push to GitHub
cd r2c2-voice-coach
git init
git add .
git commit -m "R2C2 Voice Coach"
# Create repo on GitHub, then:
git remote add origin YOUR_GITHUB_URL
git push -u origin main

# 2. Go to render.com
# - Sign up
# - New Web Service
# - Connect GitHub repo
# - Configure as shown above
# - Deploy

# 3. Deploy frontend
cd client
# Update .env.local with Render URL
vercel --prod
```

**Total time: 15-20 minutes**
**No Docker needed!**

---

## Need Help?

- **Render issues**: Check https://render.com/docs
- **Vercel issues**: Check https://vercel.com/docs
- **Ngrok issues**: Check https://ngrok.com/docs

**Choose the method that works best for you!**
