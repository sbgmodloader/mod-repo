# Super Battle Golf Mods Repository

**Official mod repository for Super Battle Golf Mod Loader**

Browse and download mods directly from the launcher, or explore here on GitHub!

## 🌐 Repository URL

```
https://sbgmods.github.io/repository/index.json
```

This URL is used by the mod loader's "Browse Mods" feature.

## 📦 Available Mods

Currently hosting **1** mod(s):

### Featured Mods
- **Example Desert Course** - A sample 9-hole desert themed course (Map)

See [index.json](index.json) for the complete catalog.

## 📥 How to Use

### Option 1: In-Game Browser (Recommended)
1. Open **SBG Mod Launcher**
2. Click **"🌐 Browse Mods"**
3. Browse, search, and install with one click!

### Option 2: Manual Download
1. Browse `mods/` folder
2. Download the ZIP file
3. Extract to your `Mods/` folder
4. Refresh mods in launcher

## 📤 Submit Your Mod

Want to share your creation with the community?

### Quick Submission Process

1. **Prepare your mod:**
   - Must have valid `mod.json`
   - Test it works in-game
   - Create a thumbnail (optional but recommended)
   - Write a good description

2. **Fork this repository:**
   ```bash
   git clone https://github.com/sbgmods/repository.git
   cd repository
   ```

3. **Add your mod:**
   ```bash
   # Create mod directory
   mkdir -p mods/your-mod-id/1.0.0
   
   # Copy your mod ZIP
   cp ~/YourMod.zip mods/your-mod-id/1.0.0/your-mod-id.zip
   
   # (Optional) Add thumbnail
   cp ~/thumbnail.jpg thumbs/your-mod-id.jpg
   ```

4. **Update index.json:**
   Add your mod entry (see format below)

5. **Create Pull Request:**
   - Push to your fork
   - Open PR to main repository
   - Wait for review (usually 1-2 days)

### Mod Entry Format

```json
{
  "id": "your-mod-id",
  "name": "Your Mod Name",
  "author": "YourUsername",
  "version": "1.0.0",
  "description": "A detailed description of what your mod does",
  "type": "map",
  "downloads": 0,
  "rating": 0.0,
  "ratingCount": 0,
  "featured": false,
  "updatedDate": "2026-04-14",
  "tags": ["tag1", "tag2", "tag3"],
  "thumbnailUrl": "https://sbgmods.github.io/repository/thumbs/your-mod-id.jpg",
  "downloadUrl": "https://sbgmods.github.io/repository/mods/your-mod-id/1.0.0/your-mod-id.zip",
  "fileSize": 1048576,
  "minLoaderVersion": "1.0.0"
}
```

**Field Guidelines:**
- `id`: Lowercase, kebab-case, unique (e.g., "awesome-volcano-map")
- `type`: One of: `map`, `gamemode`, `character`, `item`
- `tags`: Descriptive, lowercase, max 5 tags
- `fileSize`: In bytes (get with `Get-Item yourmod.zip | Select-Object Length`)
- `thumbnailUrl`: 1280x720 recommended, JPG/PNG, max 500KB

See [SUBMISSION_GUIDE.md](SUBMISSION_GUIDE.md) for detailed instructions.

## ✅ Automated Validation

All submissions are automatically validated by GitHub Actions:

- ✅ Valid JSON syntax
- ✅ All required fields present
- ✅ Unique mod ID
- ✅ File size limits (< 100MB per mod)
- ✅ Valid mod.json inside ZIP
- ✅ No malicious files
- ✅ Proper version format

Failed checks will be commented on your PR with fix instructions.

## 📋 Submission Guidelines

### ✅ Allowed
- Custom maps, game modes, characters, items
- SFW content only
- Original creations
- Ports/remixes with permission
- Mods that enhance gameplay

### ❌ Not Allowed
- NSFW/inappropriate content
- Copyrighted material without permission
- Malicious code or viruses
- Mods that violate game TOS
- Low-effort content
- Mods that harm game balance (competitive)

### Quality Standards
- Must work with latest mod loader version
- Include clear description
- Proper credits to assets used
- No game-breaking bugs
- Testing required before submission

## 🎯 Getting Featured

Featured mods appear at the top of the browser! Criteria:
- ⭐ High quality (5+ ratings, 4.5+ average)
- 📥 Popular (100+ downloads)
- 🎨 Has thumbnail
- 📝 Good description
- 🔄 Actively maintained

Moderators review for featuring monthly.

## 🔄 Updating Your Mod

To release an update:

1. Create new version directory:
   ```bash
   mkdir -p mods/your-mod-id/1.1.0
   cp YourMod-v1.1.0.zip mods/your-mod-id/1.1.0/your-mod-id.zip
   ```

2. Update `index.json`:
   - Change `version` to `1.1.0`
   - Update `downloadUrl` path
   - Update `updatedDate`
   - Increment `fileSize` if changed

3. Submit PR

Old versions are kept for compatibility.

## 📊 Statistics

Stats are updated automatically:
- **Downloads**: Incremented when users install via launcher
- **Ratings**: Users can rate mods (coming soon)
- **Featured**: Manually curated by moderators

## 🛠️ Repository Structure

```
repository/
├── index.json              # Main catalog (DO THIS FIRST!)
├── mods/
│   └── your-mod-id/
│       ├── 1.0.0/
│       │   └── your-mod-id.zip
│       └── 1.1.0/
│           └── your-mod-id.zip
├── thumbs/
│   └── your-mod-id.jpg     # Thumbnail (optional)
├── .github/
│   └── workflows/
│       └── validate.yml    # Auto-validation
└── README.md
```

## 🚀 Local Testing

Test your mod entry locally before submitting:

```bash
# Validate JSON syntax
python -m json.tool index.json

# Test download URL
curl -I https://sbgmods.github.io/repository/mods/your-mod-id/1.0.0/your-mod-id.zip

# Test in launcher
# Point repository URL to your fork temporarily
```

## ❓ FAQ

**Q: How long does review take?**  
A: Usually 1-2 days. Complex mods may take longer.

**Q: Can I update download counts manually?**  
A: No, these are tracked automatically by the launcher.

**Q: My PR was rejected, why?**  
A: Check the automated comments. Common issues: invalid JSON, missing files, too large.

**Q: Can I host mods on my own site?**  
A: Yes! Fork this repo and change URLs to your hosting. Or create your own repository.

**Q: How do I delete my mod?**  
A: Open an issue requesting removal. We'll process within 24 hours.

**Q: Can I have multiple mods?**  
A: Yes! Add as many as you want. Each needs its own ID.

## 📞 Contact & Support

- **Issues**: [GitHub Issues](https://github.com/sbgmods/repository/issues)
- **Discord**: [Join our community](#)
- **Email**: mods@sbgmods.github.io

## 📜 License

- Repository structure: MIT License
- Individual mods: Licensed by their respective authors
- Always credit original creators!

## 🙏 Credits

- **Mod Loader**: [sbgmodloader](https://github.com/ssfdre38/sbgmodloader)
- **Repository Maintainers**: Community volunteers
- **Contributors**: All amazing mod creators!

---

**Happy Modding! ⛳🎮**
