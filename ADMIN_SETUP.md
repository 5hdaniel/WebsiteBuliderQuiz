# Admin Panel Setup Guide - Decap CMS

This guide explains how to set up the admin panel with authentication.

## 🎯 What You Get

After setup, you'll have:
- **Admin Panel URL**: `yoursite.com/admin`
- **Login**: Google or Microsoft account authentication
- **Editor**: Visual editor to create/edit blog posts
- **No Code Required**: Admins don't need to touch any code

---

## 🔐 How Authentication Works

### The Simple Explanation:

1. **Admin visits** `/admin`
2. **Clicks "Login with GitHub"** (or Google/Microsoft)
3. **Decap CMS checks**: "Is this person authorized?"
4. **If YES**: Admin can edit content
5. **If NO**: Access denied

### Who Can Be An Admin?

**Option 1: GitHub Repository Access (Easiest)**
- Anyone with **write access** to your GitHub repo can be admin
- Perfect for: Small teams, trusted collaborators

**Option 2: GitHub OAuth App (More Control)**
- Only specific GitHub accounts you approve
- Perfect for: Larger teams, more security

**Option 3: External Auth Providers**
- Google, Microsoft, etc. via third-party services
- Requires additional setup (more complex)

---

## 🚀 Setup Instructions

### Method 1: GitHub Backend (RECOMMENDED - Easiest)

This method uses GitHub for authentication. Anyone with write access to the repo can be an admin.

#### Step 1: Deploy to Vercel (if not already done)

Follow the DEPLOYMENT.md guide to deploy your site to Vercel.

#### Step 2: Enable GitHub OAuth in Vercel

1. Go to your **Vercel Dashboard**
2. Select your project
3. Go to **Settings** → **Git**
4. Under "GitHub OAuth", click **Connect GitHub Account**
5. Authorize Vercel to access your GitHub

#### Step 3: Update the config file

The `blog/admin/config.yml` file needs to be updated with your correct branch:

```yaml
backend:
  name: github
  repo: 5hdaniel/WebsiteBuliderQuiz
  branch: main  # ← Change this to your main branch if different
```

#### Step 4: Grant Admin Access

**To make someone an admin:**

1. Go to your GitHub repo: `https://github.com/5hdaniel/WebsiteBuliderQuiz`
2. Click **Settings** → **Collaborators**
3. Click **Add people**
4. Enter their GitHub username
5. Give them **Write** or **Admin** access

**That's it!** They can now:
1. Visit `yoursite.com/admin`
2. Click "Login with GitHub"
3. Start editing content

---

### Method 2: Netlify Identity (For Google/Microsoft Login)

If you want **Google or Microsoft authentication** instead of GitHub:

#### Prerequisites:
- Deploy to **Netlify** instead of Vercel (Netlify has built-in identity)
- OR use a third-party auth service like **Auth0** or **Clerk**

#### Steps for Netlify:

1. **Deploy to Netlify** (similar to Vercel)

2. **Enable Netlify Identity**:
   - Go to Netlify Dashboard → Your Site
   - Click **Identity** tab
   - Click **Enable Identity**

3. **Enable External Providers**:
   - In Identity settings, click **Settings and usage**
   - Scroll to **External providers**
   - Enable **Google** or **Microsoft**
   - Add OAuth credentials (from Google/Microsoft developer console)

4. **Update config.yml**:
   ```yaml
   backend:
     name: git-gateway
     branch: main
   ```

5. **Add Netlify Identity Widget** to your site:
   ```html
   <script src="https://identity.netlify.com/v1/netlify-identity-widget.js"></script>
   ```

6. **Invite admins**:
   - In Netlify Identity tab, click **Invite users**
   - Enter their email addresses
   - They'll receive invitation emails

---

## 📝 How to Use the Admin Panel

### Accessing the Admin Panel:

1. Visit: `yoursite.com/admin`
2. Click "Login with GitHub" (or your configured provider)
3. Authorize access

### Creating a New Blog Post:

1. Click **"New Blog Posts"** in the sidebar
2. Fill in the fields:
   - **Title**: Post title
   - **Publish Date**: When to publish
   - **Author**: Your name
   - **Featured Image**: Upload or select image
   - **Excerpt**: Short preview text
   - **Body**: Main content (supports Markdown)
   - **Tags**: Optional tags
   - **Category**: Select category

3. Click **"Publish"** → **"Publish now"**

4. Wait 1-2 minutes for Vercel to rebuild

5. **Your post is live!**

### Editing Existing Posts:

1. Click **"Blog Posts"** in sidebar
2. Click on the post you want to edit
3. Make changes
4. Click **"Publish"** → **"Publish now"**

### Editing About Page or Settings:

1. Click **"Pages"** in sidebar
2. Select **"About Page"** or **"Site Settings"**
3. Make changes
4. Click **"Publish"**

---

## 🔧 Configuration Details

### Current Setup:

**File**: `blog/admin/config.yml`

```yaml
backend:
  name: github
  repo: 5hdaniel/WebsiteBuliderQuiz
  branch: main
```

This means:
- **Backend**: Uses GitHub for storage
- **Repository**: Your GitHub repo
- **Branch**: Posts are committed to the main branch

### What Happens When You Publish:

1. Admin clicks "Publish" in CMS
2. Decap CMS creates a Git commit with changes
3. Commit is pushed to GitHub
4. Vercel detects the push
5. Vercel rebuilds and deploys the site
6. Changes are live (1-2 minutes)

---

## 🛡️ Security

### How It's Protected:

✅ **OAuth Authentication**: Only authorized accounts can access
✅ **GitHub Permissions**: Tied to repo access
✅ **HTTPS**: All connections encrypted
✅ **Git History**: All changes tracked and reversible
✅ **No Database**: No database to hack

### Best Practices:

1. **Use strong GitHub passwords** and enable 2FA
2. **Only invite trusted collaborators**
3. **Review commits** before pushing to production (optional)
4. **Use branch protection** to require reviews (advanced)

---

## 🎨 Customizing the Admin Panel

### Changing Fields:

Edit `blog/admin/config.yml`:

```yaml
fields:
  - {label: "Title", name: "title", widget: "string"}
  - {label: "Custom Field", name: "custom", widget: "text"}
```

Available widgets:
- `string`: Single line text
- `text`: Multi-line text
- `markdown`: Rich text editor
- `number`: Numbers
- `boolean`: True/False
- `datetime`: Date picker
- `image`: Image uploader
- `file`: File uploader
- `select`: Dropdown menu
- `list`: Repeatable items

### Adding Collections:

Add more content types (e.g., Products, Portfolio):

```yaml
collections:
  - name: "products"
    label: "Products"
    folder: "blog/products"
    create: true
    fields:
      - {label: "Name", name: "name", widget: "string"}
      - {label: "Price", name: "price", widget: "number"}
```

---

## 🐛 Troubleshooting

### "Error: Failed to load config.yml"
- **Solution**: Check that `blog/admin/config.yml` exists
- Make sure YAML formatting is correct (no tabs, proper indents)

### "Cannot read property 'name' of undefined"
- **Solution**: Update the `repo:` field in config.yml with your repo

### "Authentication failed"
- **Solution**: Check GitHub OAuth is enabled in Vercel
- Verify you have write access to the repo

### "Changes not showing on site"
- **Solution**: Wait 2-3 minutes for Vercel to rebuild
- Check Vercel deployment logs

### Admin panel shows blank page
- **Solution**: Clear browser cache
- Check browser console for errors
- Verify admin/index.html exists

---

## 📚 Additional Resources

- [Decap CMS Documentation](https://decapcms.org/docs/intro/)
- [GitHub OAuth Setup](https://docs.github.com/en/developers/apps/building-oauth-apps)
- [Vercel Git Integration](https://vercel.com/docs/concepts/git)

---

## 🎉 Quick Start Checklist

- [ ] Deploy site to Vercel
- [ ] Enable GitHub OAuth in Vercel
- [ ] Update config.yml with correct branch
- [ ] Add collaborators to GitHub repo
- [ ] Test admin access at `/admin`
- [ ] Create your first blog post!

---

**Need help?** Check the troubleshooting section or open an issue on GitHub!
