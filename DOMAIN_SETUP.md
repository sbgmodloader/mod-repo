# Custom Domain Setup for sbgmodloader.com

Complete guide for setting up custom domains for the SBG Mod Loader ecosystem.

## 🌐 Domain Architecture

```
sbgmodloader.com                    → Main landing page
www.sbgmodloader.com                → Redirects to main
mods.sbgmodloader.com               → Mod repository/browser
sdk.sbgmodloader.com                → SDK documentation
maps.sbgmodloader.com               → Map Maker documentation
launcher.sbgmodloader.com           → Launcher documentation
docs.sbgmodloader.com               → Main docs (C++ loader)
```

---

## 📋 DNS Configuration

### At Your Domain Registrar (GoDaddy, Namecheap, etc.)

Add these **CNAME records**:

| Type  | Host      | Value                      | TTL  |
|-------|-----------|----------------------------|------|
| CNAME | @         | sbgmodloader.github.io     | 3600 |
| CNAME | www       | sbgmodloader.github.io     | 3600 |
| CNAME | mods      | sbgmodloader.github.io     | 3600 |
| CNAME | sdk       | sbgmodloader.github.io     | 3600 |
| CNAME | maps      | sbgmodloader.github.io     | 3600 |
| CNAME | launcher  | sbgmodloader.github.io     | 3600 |
| CNAME | docs      | sbgmodloader.github.io     | 3600 |

**Note:** Some registrars don't allow CNAME for apex domain (@). If this happens, use **A records** instead:

| Type | Host | Value          | TTL  |
|------|------|----------------|------|
| A    | @    | 185.199.108.153 | 3600 |
| A    | @    | 185.199.109.153 | 3600 |
| A    | @    | 185.199.110.153 | 3600 |
| A    | @    | 185.199.111.153 | 3600 |

*(These are GitHub's official IP addresses)*

---

## 🚀 GitHub Pages Configuration

### 1. Create Organization Landing Page

```bash
# Create special repo for organization page
# Repo name MUST be: sbgmodloader.github.io
```

On GitHub:
1. Go to https://github.com/organizations/sbgmodloader/repositories/new
2. Repository name: `sbgmodloader.github.io`
3. Description: "Official website for Super Battle Golf Mod Loader"
4. Public visibility
5. Initialize with README
6. Create repository

Then configure:
1. Settings → Pages
2. Source: main branch / root
3. Custom domain: `sbgmodloader.com`
4. Enforce HTTPS ✅

### 2. Configure Mod Repository

For **sbgmodloader/mod-repo**:

1. Settings → Pages
2. Source: main branch / root
3. Custom domain: `mods.sbgmodloader.com`
4. Enforce HTTPS ✅

### 3. Configure SDK Repository

For **sbgmodloader/sdk**:

1. Settings → Pages
2. Source: main branch / root (or /docs folder)
3. Custom domain: `sdk.sbgmodloader.com`
4. Enforce HTTPS ✅

### 4. Configure Map Maker Repository

For **sbgmodloader/map-maker**:

1. Settings → Pages
2. Source: main branch / root (or /docs folder)
3. Custom domain: `maps.sbgmodloader.com`
4. Enforce HTTPS ✅

### 5. Configure Launcher Repository

For **sbgmodloader/launcher**:

1. Settings → Pages
2. Source: main branch / root (or /docs folder)
3. Custom domain: `launcher.sbgmodloader.com`
4. Enforce HTTPS ✅

### 6. Configure Main Docs

For **sbgmodloader/mod-loader**:

1. Settings → Pages
2. Source: main branch / /docs folder
3. Custom domain: `docs.sbgmodloader.com`
4. Enforce HTTPS ✅

---

## ✅ Verification Steps

### 1. Wait for DNS Propagation

DNS changes take 5 minutes to 48 hours (usually ~1 hour).

Check status:
```bash
# Check if DNS is propagated
nslookup mods.sbgmodloader.com
# Should return: sbgmodloader.github.io

# Or use online tool:
# https://dnschecker.org
```

### 2. Test Each Domain

Once DNS is propagated:

- ✅ http://sbgmodloader.com → Main site
- ✅ http://www.sbgmodloader.com → Redirects to main
- ✅ http://mods.sbgmodloader.com/index.json → Mod catalog
- ✅ http://sdk.sbgmodloader.com → SDK docs
- ✅ http://maps.sbgmodloader.com → Map tool docs
- ✅ http://launcher.sbgmodloader.com → Launcher docs
- ✅ http://docs.sbgmodloader.com → Main documentation

### 3. Enable HTTPS

GitHub automatically provisions SSL certificates (Let's Encrypt).

This takes **up to 24 hours** after domain verification.

Once ready, all HTTP traffic redirects to HTTPS automatically.

---

## 🔧 CNAME Files (Automated)

GitHub automatically creates a `CNAME` file in each repository when you set a custom domain.

Contents of each CNAME file:

**mod-repo/CNAME:**
```
mods.sbgmodloader.com
```

**sdk/CNAME:**
```
sdk.sbgmodloader.com
```

**map-maker/CNAME:**
```
maps.sbgmodloader.com
```

**launcher/CNAME:**
```
launcher.sbgmodloader.com
```

**mod-loader/docs/CNAME:**
```
docs.sbgmodloader.com
```

**sbgmodloader.github.io/CNAME:**
```
sbgmodloader.com
```

**Important:** Don't delete these files! GitHub needs them.

---

## 🎨 Landing Page Content

Create a simple landing page at **sbgmodloader/sbgmodloader.github.io**:

```html
<!DOCTYPE html>
<html>
<head>
    <title>SBG Mod Loader - Modding for Super Battle Golf</title>
    <meta charset="utf-8">
    <style>
        body {
            font-family: Arial, sans-serif;
            background: #1A1D23;
            color: #E8E9ED;
            text-align: center;
            padding: 50px;
        }
        h1 { color: #4CAF50; }
        a {
            color: #2196F3;
            text-decoration: none;
            padding: 10px 20px;
            margin: 10px;
            border: 2px solid #2196F3;
            border-radius: 5px;
            display: inline-block;
        }
        a:hover { background: #2196F3; color: white; }
    </style>
</head>
<body>
    <h1>⛳ Super Battle Golf Mod Loader</h1>
    <p>The complete modding solution for Super Battle Golf</p>
    
    <div>
        <a href="https://mods.sbgmodloader.com">Browse Mods</a>
        <a href="https://sdk.sbgmodloader.com">SDK Docs</a>
        <a href="https://maps.sbgmodloader.com">Map Maker</a>
        <a href="https://docs.sbgmodloader.com">Documentation</a>
        <a href="https://github.com/sbgmodloader">GitHub</a>
    </div>
</body>
</html>
```

---

## 🔄 Update Launcher Code

Already done! Updated in `ModRepositoryService.cs`:

```csharp
public ModRepositoryService(string repositoryUrl = "https://mods.sbgmodloader.com")
```

Rebuild launcher after DNS is live!

---

## 📊 Benefits of Custom Domains

✅ **Professional branding** - sbgmodloader.com vs github.io
✅ **Easy to remember** - Users type "sbgmodloader.com"
✅ **Better SEO** - Custom domains rank higher
✅ **Flexibility** - Can change hosting without breaking URLs
✅ **Free SSL** - GitHub provides automatic HTTPS
✅ **Subdomains** - Organize ecosystem cleanly

---

## 🆘 Troubleshooting

### "Domain is improperly configured"

- Wait longer (DNS can take 24-48 hours)
- Check DNS records at registrar
- Ensure CNAME points to sbgmodloader.github.io
- Remove any conflicting A records

### "Certificate provisioning failed"

- GitHub can take up to 24 hours to issue SSL
- Ensure domain is verified (check Settings → Pages)
- Try removing and re-adding custom domain

### "404 Not Found"

- Ensure GitHub Pages is enabled
- Check source branch is correct
- Wait a few minutes after enabling

### "Too many redirects"

- Don't add both apex (@) CNAME and A records
- Use one or the other, not both

---

## 📚 References

- **GitHub Pages Docs:** https://docs.github.com/en/pages
- **Custom Domains:** https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site
- **DNS Checker:** https://dnschecker.org
- **SSL Status:** https://www.ssllabs.com/ssltest/

---

**DNS propagation typically takes 1-2 hours.** Be patient!

After that, your entire ecosystem will be accessible via:
**sbgmodloader.com** and its subdomains! 🎉
