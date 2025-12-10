---
description: Deploy to Cloudflare Pages
---

# Deploy Rembayung to Cloudflare Pages

This workflow guides you through deploying the Rembayung restaurant website to Cloudflare Pages.

## Prerequisites

1. A Cloudflare account (free tier works fine)
2. Wrangler CLI installed (Cloudflare's command-line tool)

## Method 1: Direct Upload via Wrangler CLI (Recommended)

### Step 1: Install Wrangler CLI

```bash
npm install -g wrangler
```

### Step 2: Login to Cloudflare

```bash
wrangler login
```

This will open a browser window for you to authenticate with Cloudflare.

### Step 3: Deploy the site

```bash
wrangler pages deploy . --project-name=rembayung
```

This will:
- Create a new Cloudflare Pages project called "rembayung" (if it doesn't exist)
- Upload all files in the current directory
- Deploy your site
- Give you a URL like: `https://rembayung.pages.dev`

### Step 4: (Optional) Set up a custom domain

1. Go to your Cloudflare Pages dashboard
2. Select your project
3. Go to "Custom domains"
4. Add your domain

## Method 2: Git Integration (Automatic Deployments)

### Step 1: Initialize Git (if not already done)

```bash
git init
git add .
git commit -m "Initial commit - Rembayung restaurant website"
```

### Step 2: Create a GitHub repository

1. Go to GitHub and create a new repository
2. Follow the instructions to push your code:

```bash
git remote add origin https://github.com/YOUR_USERNAME/rembayung.git
git branch -M main
git push -u origin main
```

### Step 3: Connect to Cloudflare Pages

1. Go to [Cloudflare Pages Dashboard](https://dash.cloudflare.com/?to=/:account/pages)
2. Click "Create a project"
3. Click "Connect to Git"
4. Select your repository
5. Configure build settings:
   - **Build command:** Leave empty (static site)
   - **Build output directory:** `/` (root directory)
6. Click "Save and Deploy"

## Method 3: Manual Upload via Dashboard

### Step 1: Create a deployment package

```bash
zip -r rembayung-deploy.zip . -x "*.git*" -x "*.vscode*" -x "*.agent*" -x "branding.md" -x "landingpage.png"
```

### Step 2: Upload via Dashboard

1. Go to [Cloudflare Pages Dashboard](https://dash.cloudflare.com/?to=/:account/pages)
2. Click "Create a project"
3. Click "Upload assets"
4. Upload the zip file or drag and drop your files
5. Name your project "rembayung"
6. Click "Deploy site"

## Post-Deployment

After deployment, you'll get a URL like:
- Production: `https://rembayung.pages.dev`
- Each deployment also gets a unique preview URL

### Environment Variables (if needed)

If you need to add environment variables:
1. Go to your project settings
2. Navigate to "Environment variables"
3. Add your variables

### Custom Domain Setup

1. In your Cloudflare Pages project, go to "Custom domains"
2. Click "Set up a custom domain"
3. Enter your domain name
4. Follow the DNS configuration instructions

## Troubleshooting

### Issue: Images not loading
- Make sure the `images` folder is included in the deployment
- Check that image paths in `index.html` are relative (they are)

### Issue: CDN resources not loading
- The site uses CDN links for Tailwind, Alpine.js, and Motion.js
- These should work fine, but ensure your CSP settings allow external scripts

### Issue: Dark mode not persisting
- This is client-side only and should work fine
- No server-side configuration needed

## Performance Optimization

Cloudflare Pages automatically provides:
- ✅ Global CDN
- ✅ Automatic HTTPS
- ✅ Unlimited bandwidth (on free tier)
- ✅ DDoS protection
- ✅ Automatic minification (can be enabled in settings)

## Recommended: Enable Additional Optimizations

1. Go to your project settings
2. Enable "Auto Minify" for HTML, CSS, and JavaScript
3. Enable "Brotli compression"
4. Enable "HTTP/3 (with QUIC)"

## Updating Your Site

### With Wrangler CLI:
```bash
wrangler pages deploy . --project-name=rembayung
```

### With Git Integration:
```bash
git add .
git commit -m "Update site"
git push
```

The site will automatically redeploy on every push to your main branch.
