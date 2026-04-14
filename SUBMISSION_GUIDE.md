# Mod Submission Guide

Complete guide for submitting mods to the Super Battle Golf Mods Repository.

## 📋 Table of Contents

1. [Before You Start](#before-you-start)
2. [Preparing Your Mod](#preparing-your-mod)
3. [Creating Your Submission](#creating-your-submission)
4. [Testing Locally](#testing-locally)
5. [Submitting Pull Request](#submitting-pull-request)
6. [After Submission](#after-submission)
7. [Troubleshooting](#troubleshooting)

---

## Before You Start

### Requirements

- ✅ GitHub account
- ✅ Git installed
- ✅ Your mod tested and working
- ✅ Valid mod.json file
- ✅ SBG Mod Loader v1.0.0+

### Recommended Tools

- **Text Editor**: VS Code, Notepad++, or similar
- **Image Editor**: For thumbnails (GIMP, Photoshop, Paint.NET)
- **JSON Validator**: https://jsonlint.com

---

## Preparing Your Mod

### 1. Test Your Mod Thoroughly

```bash
# In SBG Mod Launcher:
1. Add your mod to Mods/[Type]/YourMod/
2. Refresh mods
3. Enable your mod
4. Launch game with mods
5. Verify everything works
```

**Test checklist:**
- [ ] Mod loads without errors
- [ ] No crashes or freezes
- [ ] Assets display correctly
- [ ] Gameplay works as intended
- [ ] No conflicts with other mods

### 2. Validate mod.json

Your mod **must** have a valid `mod.json`:

```json
{
  "id": "your-mod-id",
  "name": "Your Mod Name",
  "version": "1.0.0",
  "author": "YourName",
  "description": "What your mod does",
  "type": "map",
  "loader_version": "1.0.0"
}
```

**Validate it:**
```bash
# Check syntax
python -m json.tool YourMod/mod.json

# Or use online: https://jsonlint.com
```

### 3. Create ZIP Package

```bash
# Folder structure BEFORE zipping:
YourMod/
├── mod.json
├── catalog.bin              # For maps
├── [mod_files]
└── README.md (optional)

# Create ZIP:
# Windows PowerShell:
Compress-Archive -Path YourMod\* -DestinationPath your-mod-id.zip

# The ZIP should contain files directly, NOT a folder:
# ✅ CORRECT:
#    your-mod-id.zip
#    ├── mod.json
#    └── catalog.bin
# 
# ❌ WRONG:
#    your-mod-id.zip
#    └── YourMod/
#        ├── mod.json
#        └── catalog.bin
```

**File size limits:**
- Maps: < 100 MB
- Game Modes: < 10 MB
- Characters: < 50 MB
- Items: < 50 MB

### 4. Create Thumbnail (Optional but Recommended)

**Specs:**
- Resolution: 1280x720 (16:9)
- Format: JPG or PNG
- Max size: 500 KB
- Content: Screenshot of your mod in-game

**Tips:**
- Capture best angle of your map/character
- Use high graphics settings
- No UI visible (hide HUD)
- Bright, clear, appealing

---

## Creating Your Submission

### Step 1: Fork Repository

```bash
# On GitHub:
1. Go to https://github.com/sbgmods/repository
2. Click "Fork" button (top right)
3. Clone YOUR fork:

git clone https://github.com/YourUsername/repository.git
cd repository
```

### Step 2: Create Mod Directory

```bash
# Navigate to mods folder
cd mods

# Create your mod's folder structure
mkdir -p your-mod-id/1.0.0
```

**Naming rules for mod ID:**
- Lowercase only
- Use hyphens for spaces
- No special characters
- Must be unique
- Examples:
  - ✅ `volcano-extreme-map`
  - ✅ `battle-royale-v2`
  - ✅ `neon-character-pack`
  - ❌ `My_Awesome_Map!`
  - ❌ `map123`

### Step 3: Add Your Files

```bash
# Copy your mod ZIP
cp ~/Desktop/your-mod-id.zip mods/your-mod-id/1.0.0/your-mod-id.zip

# Copy thumbnail (if you have one)
cp ~/Desktop/thumbnail.jpg thumbs/your-mod-id.jpg
```

**Verify file names match:**
```
mods/volcano-map/1.0.0/volcano-map.zip  ✅
mods/volcano-map/1.0.0/VolcanoMap.zip   ❌

thumbs/volcano-map.jpg                   ✅
thumbs/volcano_map.jpg                   ❌
```

### Step 4: Get File Size

```powershell
# Windows PowerShell:
(Get-Item mods\your-mod-id\1.0.0\your-mod-id.zip).Length

# Example output: 5242880 (bytes)
```

### Step 5: Edit index.json

Open `index.json` and add your mod entry to the `"mods"` array:

```json
{
  "version": "1.0.0",
  "updated": "2026-04-14",
  "mods": [
    {
      "id": "your-mod-id",
      "name": "Your Mod Name",
      "author": "YourUsername",
      "version": "1.0.0",
      "description": "A detailed, engaging description of what your mod adds to the game. Be specific and highlight unique features!",
      "type": "map",
      "downloads": 0,
      "rating": 0.0,
      "ratingCount": 0,
      "featured": false,
      "updatedDate": "2026-04-14",
      "tags": ["volcano", "challenging", "18-hole", "hazards"],
      "thumbnailUrl": "https://sbgmods.github.io/repository/thumbs/your-mod-id.jpg",
      "downloadUrl": "https://sbgmods.github.io/repository/mods/your-mod-id/1.0.0/your-mod-id.zip",
      "fileSize": 5242880,
      "minLoaderVersion": "1.0.0"
    }
  ]
}
```

**Field-by-field guide:**

| Field | Required | Description | Example |
|-------|----------|-------------|---------|
| `id` | ✅ | Unique identifier (kebab-case) | `"volcano-extreme-map"` |
| `name` | ✅ | Display name | `"Volcano Extreme Map"` |
| `author` | ✅ | Your username | `"ModMaster"` |
| `version` | ✅ | Semantic version | `"1.0.0"` |
| `description` | ✅ | What it does (100-300 chars) | `"A challenging 9-hole course through an active volcano..."` |
| `type` | ✅ | Mod category | `"map"`, `"gamemode"`, `"character"`, `"item"` |
| `downloads` | ✅ | Start at 0 | `0` |
| `rating` | ✅ | Start at 0.0 | `0.0` |
| `ratingCount` | ✅ | Start at 0 | `0` |
| `featured` | ✅ | Start false | `false` |
| `updatedDate` | ✅ | Today's date (YYYY-MM-DD) | `"2026-04-14"` |
| `tags` | ✅ | 3-5 descriptive tags | `["volcano", "challenging", "9-hole"]` |
| `thumbnailUrl` | ⚠️ | URL to thumbnail (or `""`) | Full URL as shown |
| `downloadUrl` | ✅ | URL to ZIP | Full URL as shown |
| `fileSize` | ✅ | Bytes (from Step 4) | `5242880` |
| `minLoaderVersion` | ✅ | Min mod loader version | `"1.0.0"` |

**URL Templates:**
```
Thumbnail: https://sbgmods.github.io/repository/thumbs/[MOD-ID].jpg
Download:  https://sbgmods.github.io/repository/mods/[MOD-ID]/[VERSION]/[MOD-ID].zip
```

Replace `[MOD-ID]` and `[VERSION]` with your values.

### Step 6: Update Repository Date

In `index.json`, update the `"updated"` field at the top to today's date:

```json
{
  "version": "1.0.0",
  "updated": "2026-04-14",  ← Change this
  "mods": [...]
}
```

---

## Testing Locally

### Validate JSON

```bash
# Check for syntax errors
python -m json.tool index.json

# Should output the JSON if valid
# Will show error line if invalid
```

**Common JSON errors:**
- Missing comma after entry
- Extra comma on last entry
- Mismatched quotes (`"` vs `'`)
- Unclosed brackets

### Test ZIP Contents

```bash
# Extract and verify
unzip -l mods/your-mod-id/1.0.0/your-mod-id.zip

# Should see mod.json in root
```

### Preview Locally (Advanced)

```bash
# Serve repository locally
python -m http.server 8000

# In mod launcher, temporarily change repository URL to:
http://localhost:8000/index.json

# Test browsing and downloading
```

---

## Submitting Pull Request

### Step 1: Commit Changes

```bash
git add index.json mods/ thumbs/
git commit -m "Add [Your Mod Name] v1.0.0

- Type: [map/gamemode/character/item]
- Description: [Brief description]
- Features: [Key features]
- Tested with Mod Loader v1.0.0"

git push origin main
```

### Step 2: Create PR on GitHub

1. Go to **your fork** on GitHub
2. Click **"Pull requests"** tab
3. Click **"New pull request"**
4. Base repository: `sbgmods/repository` ← `YourUsername/repository`
5. Click **"Create pull request"**

### Step 3: Fill Out PR Template

```markdown
## Mod Submission

**Mod Name:** Your Mod Name
**Type:** Map
**Version:** 1.0.0
**Author:** YourUsername

### Description
A brief description of what your mod does and why it's cool.

### Testing
- [x] Tested in-game
- [x] No crashes
- [x] mod.json validated
- [x] JSON syntax checked
- [x] File size within limits

### Screenshots
(Optional: Add in-game screenshots here)

### Additional Notes
Any extra info for reviewers.
```

---

## After Submission

### Automated Validation

GitHub Actions will automatically:
- ✅ Validate JSON syntax
- ✅ Check file sizes
- ✅ Verify mod.json exists in ZIP
- ✅ Check for malicious files
- ✅ Verify unique mod ID

Results appear as comments on your PR within ~2 minutes.

### Manual Review

A maintainer will review within 1-2 days:
- Quality check
- Description review
- Compatibility verification
- Final approval

### If Changes Requested

1. Make fixes in your fork
2. Commit and push
3. PR updates automatically
4. Wait for re-review

### After Merge

- 🎉 Your mod is live!
- Download URL active immediately
- Appears in mod browser within minutes
- Users can install with one click

---

## Updating Your Mod

### Version Update Process

```bash
# 1. Create new version directory
mkdir -p mods/your-mod-id/1.1.0
cp your-mod-id-v1.1.0.zip mods/your-mod-id/1.1.0/your-mod-id.zip

# 2. Update index.json
# Change ONLY these fields for your mod:
# - "version": "1.1.0"
# - "downloadUrl": .../ 1.1.0/...
# - "updatedDate": "2026-04-15"
# - "fileSize": [new size]

# 3. Commit and PR
git add index.json mods/
git commit -m "Update [Mod Name] to v1.1.0"
git push origin main
```

---

## Troubleshooting

### "JSON syntax error"

```bash
# Run validator
python -m json.tool index.json

# Look for line number in error
# Common fixes:
# - Add missing comma
# - Remove trailing comma
# - Fix quote mismatch
```

### "File not found (404)"

- Check file path matches URL exactly
- Verify file is in correct folder
- Check spelling/capitalization
- Wait 5 minutes for GitHub Pages to update

### "ZIP doesn't contain mod.json"

```bash
# Check ZIP contents
unzip -l your-mod.zip | grep mod.json

# Should see:
#   0  2026-04-14 mod.json  ← Good!
#   0  2026-04-14 YourMod/mod.json  ← Bad! (has folder)

# Fix: Re-zip without parent folder
```

### "File size too large"

- Compress textures (use JPG instead of PNG)
- Reduce audio quality
- Remove unnecessary files
- Split into multiple mods if needed

### "Mod ID already exists"

- Choose a different, unique ID
- Check index.json for duplicates
- Add suffix: `-v2`, `-remake`, `-yourname`

---

## Need Help?

- **Discord**: Ask in #mod-submissions
- **GitHub Issues**: [Create issue](https://github.com/sbgmods/repository/issues)
- **Email**: mods@sbgmods.github.io

---

**Good luck with your submission! 🎉**
