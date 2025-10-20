# Vercel Frontend Deployment Guide

## Prerequisites

1. Install Vercel CLI (if not already installed):
```bash
npm install -g vercel
```

2. Login to Vercel:
```bash
vercel login
```

## Deployment Steps

### Option 1: Deploy via Vercel CLI (Recommended for first deployment)

1. Navigate to the client directory:
```bash
cd r2c2-voice-coach/client
```

2. Deploy to Vercel:
```bash
vercel
```

Follow the prompts:
- Set up and deploy? **Y**
- Which scope? Select your account
- Link to existing project? **N** (for first deployment)
- What's your project's name? **r2c2-voice-coach** (or your preferred name)
- In which directory is your code located? **./** 
- Want to override the settings? **N**

3. For production deployment:
```bash
vercel --prod
```

### Option 2: Deploy via Vercel Dashboard

1. Go to [vercel.com](https://vercel.com)
2. Click "Add New Project"
3. Import your Git repository
4. Configure:
   - **Framework Preset**: Next.js
   - **Root Directory**: `client`
   - **Build Command**: `npm run build`
   - **Output Directory**: `.next`
   - **Install Command**: `npm install`

## Environment Variables

After deployment, configure these environment variables in Vercel Dashboard:

### Required Variables:

1. `BOT_START_URL` - Your backend bot start endpoint
   - Example: `https://your-backend.onrender.com/start`

2. `NEXT_PUBLIC_API_BASE_URL` - Your backend API base URL
   - Example: `https://your-backend.onrender.com`

### Optional Variables:

3. `BOT_START_PUBLIC_API_KEY` - If using Pipecat Cloud
4. `NEXT_PUBLIC_ENABLE_EMOTION_VIZ` - `true` or `false`
5. `NEXT_PUBLIC_ENABLE_PLAN_EDITING` - `true` or `false`
6. `NEXT_PUBLIC_ENABLE_SESSION_EXPORT` - `true` or `false`
7. `NEXT_PUBLIC_DEBUG_MODE` - `false` for production
8. `NEXT_PUBLIC_AUTO_SCROLL_TRANSCRIPT` - `true` or `false`

### Setting Environment Variables:

**Via Vercel Dashboard:**
1. Go to your project settings
2. Navigate to "Environment Variables"
3. Add each variable with appropriate values
4. Redeploy to apply changes

**Via Vercel CLI:**
```bash
vercel env add NEXT_PUBLIC_API_BASE_URL
# Enter the value when prompted
```

## Post-Deployment

1. **Test the deployment:**
   - Visit your Vercel URL (e.g., `https://r2c2-voice-coach.vercel.app`)
   - Verify the UI loads correctly
   - Test the connection to your backend

2. **Update backend CORS settings:**
   - Add your Vercel domain to the backend's allowed origins
   - Update `ALLOWED_ORIGINS` in your backend `.env` file

3. **Custom Domain (Optional):**
   - Go to Project Settings > Domains
   - Add your custom domain
   - Follow DNS configuration instructions

## Troubleshooting

### Build Fails
- Check build logs in Vercel dashboard
- Verify all dependencies are in `package.json`
- Ensure Node.js version compatibility

### Environment Variables Not Working
- Variables starting with `NEXT_PUBLIC_` are exposed to the browser
- Other variables are only available server-side
- Redeploy after adding/changing environment variables

### Backend Connection Issues
- Verify `NEXT_PUBLIC_API_BASE_URL` is correct
- Check backend CORS configuration
- Ensure backend is deployed and accessible

## Continuous Deployment

Vercel automatically deploys:
- **Production**: When you push to `main` branch
- **Preview**: For pull requests and other branches

To disable auto-deployment:
1. Go to Project Settings > Git
2. Configure deployment branches

## Useful Commands

```bash
# Deploy to preview
vercel

# Deploy to production
vercel --prod

# View deployment logs
vercel logs

# List deployments
vercel ls

# Remove deployment
vercel rm [deployment-url]
```

## Next Steps

1. Deploy your backend (if not already deployed)
2. Update environment variables with backend URLs
3. Test the full application flow
4. Set up custom domain (optional)
5. Configure analytics (optional)
