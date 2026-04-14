# Mod Repository Setup Instructions

Step-by-step guide to deploy the Super Battle Golf Mods Repository.

## 📋 Quick Setup (10 minutes)

### Step 1: Create GitHub Repository

1. Go to https://github.com and sign in
2. Click **"+"** → **"New repository"**
3. Settings:
   - Owner: `sbgmods` (or your username)
   - Repository name: `repository`
   - Description: `Official mod repository for Super Battle Golf Mod Loader`
   - Visibility: **Public** ✅
   - ❌ Do NOT initialize with README (we already have one)
4. Click **"Create repository"**

### Step 2: Push Repository

```bash
cd D:\sbgmods-repository

# Add remote
git remote add origin https://github.com/sbgmods/repository.git

# Push
git branch -M main
git push -u origin main
```

### Step 3: Enable GitHub Pages

1. Go to repository **Settings**
2. Scroll to **Pages** (left sidebar)
3. Source: **Deploy from a branch**
4. Branch: **main** / **root**
5. Click **Save**

Wait 2-3 minutes for deployment...

### Step 4: Verify Deployment

Visit: https://sbgmods.github.io/repository/index.json

You should see the JSON index!

### Step 5: Update Mod Loader

In `GUILauncher/Services/ModRepositoryService.cs`:

```csharp
private const string REPOSITORY_URL = "https://sbgmods.github.io/repository";
```

Rebuild launcher and you're done! 🎉

---

## 🔧 Configuration Options

### Custom Domain (Optional)

If you own a domain (e.g., `mods.sbg.com`):

1. Go to repository **Settings** → **Pages**
2. Enter **Custom domain**: `mods.sbg.com`
3. Click **Save**
4. Add DNS records at your registrar:
   - CNAME: `mods` → `sbgmods.github.io`
5. Wait for DNS propagation (~1 hour)

### Repository Organization

**Option A: Under personal account**
- URL: `https://yourusername.github.io/repository`
- Simple, works immediately
- Good for testing

**Option B: GitHub Organization (Recommended)**
- Create organization: `sbgmods`
- Transfer repository to organization
- URL: `https://sbgmods.github.io/repository`
- Professional, collaborative
- Multiple maintainers

---

## 👥 Team Setup (For Organizations)

### Add Maintainers

1. Go to organization **People**
2. Click **Invite member**
3. Enter GitHub username
4. Role: **Member** or **Owner**

### Set Repository Permissions

1. Repository **Settings** → **Manage access**
2. **Collaborators** section
3. Add team members with:
   - **Write** access: Can approve PRs
   - **Admin** access: Can manage settings

### Branch Protection

1. **Settings** → **Branches**
2. **Add branch protection rule**
3. Branch name: `main`
4. Enable:
   - ✅ Require pull request reviews (1 approval)
   - ✅ Require status checks (validation workflow)
   - ✅ Require branches to be up to date
5. **Create**

Now all submissions require PR + approval!

---

## 🤖 Automated Validation

The GitHub Actions workflow runs automatically on:
- ✅ All pull requests
- ✅ Pushes to main branch

### What It Checks

1. **JSON Syntax** - Valid JSON format
2. **Schema Validation** - All required fields present
3. **Unique IDs** - No duplicate mod IDs
4. **File Existence** - ZIP files exist at specified paths
5. **File Sizes** - Match claimed sizes, under limits
6. **Version Format** - Semantic versioning (X.Y.Z)
7. **Malicious Files** - No .exe, .dll, etc.

### Viewing Results

1. Go to **Pull Requests**
2. Click on a PR
3. Scroll to **Checks** section
4. See validation results
5. ✅ Green = passed, ❌ Red = failed

---

## 📊 Tracking Downloads (Optional)

To track download counts, you can:

### Option 1: GitHub API

Use GitHub's download API:
```bash
curl https://api.github.com/repos/sbgmods/repository/traffic/popular/paths
```

Pros: Free, simple
Cons: Only tracks last 14 days

### Option 2: Third-Party Analytics

Use services like:
- **Plausible** (privacy-friendly, $9/month)
- **Google Analytics** (free, but privacy concerns)
- **Cloudflare Analytics** (free with Cloudflare)

Add tracking script to index.json (not recommended) or use CDN.

### Option 3: Custom Redirect

```bash
# Instead of direct links, use:
https://mods.sbg.com/download/mod-id/1.0.0

# Server logs download, then redirects to:
https://sbgmods.github.io/repository/mods/mod-id/1.0.0/mod-id.zip
```

Requires custom server, but full analytics.

---

## 🚀 Scaling & Performance

### CDN (For High Traffic)

If you expect >10,000 downloads/month:

1. **Cloudflare** (Free tier):
   - Add domain to Cloudflare
   - Enable caching
   - Auto-minify JSON
   - DDoS protection

2. **jsDelivr** (Free CDN for GitHub):
   ```
   https://cdn.jsdelivr.net/gh/sbgmods/repository@main/index.json
   ```

### Large Mods (>100MB)

For mods exceeding GitHub's limits:

**Option 1: GitHub Releases**
- Upload large files as release assets
- Update downloadUrl to release URL
- 2GB limit per file

**Option 2: External Hosting**
- Google Drive (not recommended - rate limits)
- Dropbox
- MEGA
- Self-hosted server

**Option 3: Torrents**
- Create magnet link
- Include in downloadUrl
- Community seeding required

---

## 🔒 Security Best Practices

### Virus Scanning

Before merging PRs:

1. Download the mod ZIP
2. Upload to https://www.virustotal.com
3. Wait for scan results (70+ engines)
4. Only merge if 0-1 detections (false positives happen)

### Manual Review Checklist

- [ ] JSON syntax valid (automated)
- [ ] Mod ID unique (automated)
- [ ] Description appropriate (manual)
- [ ] No copyrighted content (manual)
- [ ] mod.json exists in ZIP (automated)
- [ ] Mod actually works (manual testing)
- [ ] No malicious files (automated + manual)
- [ ] File size reasonable (automated)

### Moderator Tools

Create a `MODERATORS.md` with:
- Review checklist
- Approval process
- Ban criteria
- Contact info

---

## 📈 Maintenance

### Weekly Tasks

- [ ] Review pending PRs
- [ ] Update download counts (if tracking)
- [ ] Check for broken links
- [ ] Remove DMCA takedown requests

### Monthly Tasks

- [ ] Review featured mods
- [ ] Update README with stats
- [ ] Clear old thumbnails (unused)
- [ ] Backup repository

### As Needed

- [ ] Handle abuse reports
- [ ] Update submission guidelines
- [ ] Improve validation workflow
- [ ] Community surveys

---

## 📞 Support Channels

Set up community support:

### Discord Server

Create channels:
- `#mod-showcase` - Share creations
- `#mod-submissions` - Help with PRs
- `#technical-help` - Mod loader issues
- `#repository-updates` - Announcements

### GitHub Discussions

Enable in repository settings:
- **Ideas** - Feature requests
- **Q&A** - How-to questions
- **Show and Tell** - Mod showcases

### Issue Templates

Create `.github/ISSUE_TEMPLATE/`:
- `bug_report.md` - Broken mods
- `feature_request.md` - New features
- `mod_report.md` - Report inappropriate content

---

## 🎯 Launch Checklist

Before going live:

- [ ] Repository created and public
- [ ] GitHub Pages enabled
- [ ] index.json accessible
- [ ] Example mod added (optional)
- [ ] README.md complete
- [ ] SUBMISSION_GUIDE.md clear
- [ ] GitHub Actions workflow tested
- [ ] Branch protection enabled (if org)
- [ ] Moderators added (if org)
- [ ] Discord server created
- [ ] Announcement ready
- [ ] Mod loader updated with URL

---

## 📝 First Announcement Template

```markdown
🎉 **Super Battle Golf Mod Repository is LIVE!**

Browse and install mods directly from the launcher!

🌐 **Repository URL:**
https://sbgmods.github.io/repository

📥 **How to Use:**
1. Open SBG Mod Launcher
2. Click "Browse Mods"
3. Install with one click!

📤 **Submit Your Mods:**
https://github.com/sbgmods/repository

💬 **Join Discord:**
[Your Discord invite link]

Let's build an amazing mod community! ⛳
```

Post to:
- Discord server
- Reddit (r/SuperBattleGolf)
- Game forums
- GitHub repository README

---

## 🆘 Troubleshooting

### "404 Page Not Found"

- Wait 5 minutes for GitHub Pages deployment
- Check Settings → Pages shows "Your site is published"
- Verify branch is set to `main`

### "JSON syntax error"

- Validate with `python -m json.tool index.json`
- Check for missing commas
- Remove trailing commas

### "Workflow not running"

- Check `.github/workflows/validate.yml` exists
- View Actions tab for errors
- Ensure GitHub Actions enabled in Settings

---

## 🎓 Resources

- **GitHub Pages Docs**: https://docs.github.com/en/pages
- **GitHub Actions Docs**: https://docs.github.com/en/actions
- **JSON Validator**: https://jsonlint.com
- **VirusTotal**: https://www.virustotal.com

---

**Ready to launch! 🚀**

Questions? Open an issue in the repository!
