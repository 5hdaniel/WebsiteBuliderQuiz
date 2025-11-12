# Deployment Guide - Vercel

This guide will help you deploy the blog to Vercel.

## 🚀 Quick Deploy (Easiest Method)

### Option 1: Deploy via Vercel Website (Recommended)

1. **Go to [vercel.com](https://vercel.com)** and sign up/login with GitHub

2. **Click "Add New Project"**

3. **Import your GitHub repository**
   - Select: `5hdaniel/WebsiteBuliderQuiz`

4. **Configure the project:**
   - Framework Preset: **Other**
   - Root Directory: **blog** (click "Edit" and select the blog folder)
   - Build Command: Leave empty (static site)
   - Output Directory: Leave as default

5. **Click "Deploy"**

6. **Done!** Your blog will be live at `your-project.vercel.app`

### Option 2: Deploy via Vercel CLI

```bash
# Install Vercel CLI
npm install -g vercel

# Login to Vercel
vercel login

# Navigate to the blog directory
cd blog

# Deploy
vercel

# Follow the prompts:
# - Set up and deploy? Y
# - Which scope? (select your account)
# - Link to existing project? N
# - What's your project's name? my-blog
# - In which directory is your code located? ./
# - Want to modify settings? N

# For production deployment
vercel --prod
```

## 📝 What Gets Deployed

The entire `blog/` directory will be deployed, including:
- ✅ index.html (Homepage)
- ✅ about.html (About page)
- ✅ contact.html (Contact page)
- ✅ post1.html, post2.html, post3.html (Blog posts)
- ✅ styles.css (Stylesheet)
- ✅ rss.xml (RSS feed)

## 🔧 Configuration

The `vercel.json` file is already configured with:
- Clean URLs (no .html extensions needed)
- Security headers
- Root redirect from / to /blog/

## 🌐 After Deployment

Once deployed, you'll get:
- **Live URL**: `https://your-project.vercel.app`
- **Automatic SSL**: HTTPS enabled by default
- **Global CDN**: Fast loading worldwide
- **Auto-deployments**: Pushes to the branch auto-deploy

## 📱 Custom Domain (Optional)

To add a custom domain:
1. Go to your project dashboard on Vercel
2. Click "Settings" → "Domains"
3. Add your domain and follow DNS instructions

## 🔄 Continuous Deployment

Every time you push to the branch `claude/build-user-website-011CV4ipsGxVqSrn1E1wHPNj`:
- Vercel automatically builds and deploys
- You get a preview URL for each deployment
- Previous versions are kept for rollback

## 💡 Tips

- **Preview deployments**: Every push gets a unique preview URL
- **Production branch**: Set main/master as production branch in settings
- **Environment variables**: Add in Project Settings if needed for forms
- **Analytics**: Enable Vercel Analytics in project settings (free)

## 🆘 Troubleshooting

**Issue**: Pages show 404
- **Solution**: Make sure Root Directory is set to "blog" in project settings

**Issue**: Styles not loading
- **Solution**: Check that all paths in HTML are relative (they are!)

**Issue**: Want to use main domain instead of /blog/
- **Solution**: Remove the redirect in vercel.json and move blog contents to root

## 📊 Next Steps

After deployment:
1. ✅ Test all pages and links
2. ✅ Update social media links with real URLs
3. ✅ Connect contact form to a backend (Formspree, Netlify Forms, etc.)
4. ✅ Connect newsletter to email service (Mailchimp, ConvertKit, etc.)
5. ✅ Replace placeholder images with real ones
6. ✅ Update author information
7. ✅ Add Google Analytics or Vercel Analytics

---

**Ready to deploy?** Just follow Option 1 above - it takes less than 2 minutes! 🚀
