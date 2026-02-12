# Deployment Guide - APTYOU Website

## Step 1: Push to GitHub

### If repository doesn't exist yet:
1. Go to https://github.com/apyouservices
2. Click "New repository"
3. Name: `aptyou-website`
4. Description: "Corporate website for APTYOU SERVICES PRIVATE LIMITED"
5. Choose Public or Private
6. **Don't** initialize with README
7. Click "Create repository"

### Push your code:

```bash
# If you haven't pushed yet, run:
git push -u origin main

# If you get authentication error, you may need to:
# - Use Personal Access Token instead of password
# - Or set up SSH keys
```

### Authentication Options:

**Option A: Personal Access Token (Recommended)**
1. Go to GitHub Settings → Developer settings → Personal access tokens → Tokens (classic)
2. Generate new token with `repo` scope
3. Use token as password when pushing

**Option B: SSH (More secure)**
1. Generate SSH key: `ssh-keygen -t ed25519 -C "your_email@example.com"`
2. Add to GitHub: Settings → SSH and GPG keys → New SSH key
3. Change remote URL: `git remote set-url origin git@github.com:apyouservices/aptyou-website.git`

---

## Step 2: Deploy to Vercel

### Method 1: Via Vercel Dashboard (Easiest)

1. **Sign up/Login to Vercel**
   - Go to https://vercel.com
   - Sign up with GitHub (recommended) or email

2. **Import Project**
   - Click "Add New..." → "Project"
   - Select "Import Git Repository"
   - Choose `apyouservices/aptyou-website`
   - Click "Import"

3. **Configure Project**
   - **Framework Preset:** Other (or leave as default)
   - **Root Directory:** `./` (default)
   - **Build Command:** Leave empty (static site, no build needed)
   - **Output Directory:** Leave empty (files are in root)
   - **Install Command:** Leave empty

4. **Environment Variables**
   - None needed for static site

5. **Deploy**
   - Click "Deploy"
   - Wait for deployment (usually 1-2 minutes)

6. **Custom Domain Setup**
   - After deployment, go to Project Settings → Domains
   - Add your domain: `aptyou.one`
   - Follow DNS configuration instructions
   - Update DNS records at GoDaddy:
     - Add CNAME record: `www` → `cname.vercel-dns.com`
     - Or A record: `@` → Vercel's IP (provided in dashboard)

### Method 2: Via Vercel CLI

```bash
# Install Vercel CLI
npm i -g vercel

# Login to Vercel
vercel login

# Deploy (from project directory)
vercel

# Follow prompts:
# - Set up and deploy? Yes
# - Which scope? Your account
# - Link to existing project? No
# - Project name? aptyou-website
# - Directory? ./
# - Override settings? No

# For production deployment:
vercel --prod
```

---

## Step 3: Configure Custom Domain (aptyou.one)

### In Vercel Dashboard:
1. Go to your project → Settings → Domains
2. Add domain: `aptyou.one`
3. Add domain: `www.aptyou.one` (optional, for www subdomain)

### At GoDaddy:
1. Log in to GoDaddy
2. Go to DNS Management for `aptyou.one`
3. Add/Update DNS records:

**Option A: CNAME (Recommended)**
- Type: CNAME
- Name: `www`
- Value: `cname.vercel-dns.com`
- TTL: 600

**Option B: A Record (For root domain)**
- Type: A
- Name: `@`
- Value: (Vercel will provide IP addresses)
- TTL: 600

**Note:** Vercel will show you the exact DNS records needed in the dashboard.

---

## Step 4: Verify Deployment

1. Check Vercel deployment status (should show "Ready")
2. Visit your Vercel URL: `https://aptyou-website.vercel.app`
3. After DNS propagates (can take 24-48 hours), visit `https://aptyou.one`
4. Test all pages:
   - Homepage
   - About
   - Products
   - Our Story
   - Contact
   - Privacy Policy
   - Terms

---

## Step 5: Future Updates

### To update the website:

```bash
# Make your changes locally
# Then commit and push:

git add .
git commit -m "Description of changes"
git push origin main
```

Vercel will automatically:
- Detect the push to GitHub
- Build and deploy the new version
- Update your live site (usually within 1-2 minutes)

---

## Troubleshooting

### GitHub Push Issues:
- **Authentication failed:** Use Personal Access Token
- **Repository not found:** Make sure repository exists on GitHub
- **Permission denied:** Check repository access permissions

### Vercel Deployment Issues:
- **Build failed:** Check that all files are in the repository
- **404 errors:** Ensure `index.html` is in root directory
- **CSS not loading:** Check file paths (should be relative: `styles.css`)

### DNS Issues:
- **Domain not working:** Wait 24-48 hours for DNS propagation
- **SSL certificate:** Vercel automatically provides SSL (HTTPS)
- **www redirect:** Configure in Vercel dashboard → Domains

---

## Important Notes

1. **Static Site:** No server-side code needed, perfect for Vercel
2. **Free Tier:** Vercel free tier is sufficient for this site
3. **Automatic HTTPS:** Vercel provides SSL certificates automatically
4. **Auto Deploy:** Every push to `main` branch auto-deploys
5. **Preview Deployments:** Vercel creates preview URLs for pull requests

---

## Support

- Vercel Docs: https://vercel.com/docs
- GitHub Docs: https://docs.github.com
- Contact: support@aptyou.one

