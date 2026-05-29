# 📁 Nexus Archive - JSON File System Guide

## Quick Start

### Exporting Your Data

1. Open **Nexus Archive** in your browser
2. Navigate to **Settings** (click the gear icon in the sidebar)
3. Scroll to **JSON File Export** section
4. Choose one of these options:

   **Individual Files:**
   - Click `novels.json` to export only novels
   - Click `characters.json` to export only characters
   - Click `lore.json` to export only lore entries
   - Click `chapters.json` to export only chapters
   - Click `settings.json` to export only settings

   **All Files at Once:**
   - Click **Download All JSON Files** button
   - Your browser will download 5 separate files

### Importing Your Data

1. Go to **Settings** → **JSON File Import**
2. Choose the import type:

   **Individual Files:**
   - Click "Import novels.json" and select your file
   - Click "Import characters.json" and select your file
   - (Repeat for other file types)

   **Full Backup:**
   - Click **Import Full Backup**
   - Select your `nexus-archive-backup.json` file
   - All data will be restored instantly

---

## File Organization

### Recommended Folder Structure

```
my-novel-archive/
├── index.html                      # The application
├── DATA_FILES_README.md            # Documentation
├── JSON_FILE_GUIDE.md              # This guide
│
├── exports/                        # Your exported JSON files
│   ├── novels.json
│   ├── characters.json
│   ├── lore.json
│   ├── chapters.json
│   ├── settings.json
│   └── nexus-archive-backup.json
│
└── backups/                        # Dated backups
    ├── archive-2026-01-15.json
    ├── archive-2026-01-22.json
    └── archive-2026-01-29.json
```

---

## Workflow Examples

### Daily Writing Workflow

1. **Open** `index.html` in your browser
2. **Work** on your novels, characters, and chapters
3. **Data auto-saves** to browser localStorage
4. **End of session:** Go to Settings → Export individual files
5. **Save** files to your `exports/` folder

### Weekly Backup Workflow

1. **Export all files** using "Download All JSON Files"
2. **Create dated backup:** Copy files to `backups/archive-YYYY-MM-DD/`
3. **Optional:** Commit to Git repository

### Version Control with Git

```bash
# Initialize repository
git init
git add index.html *.json *.md

# Create .gitignore
echo "node_modules/" >> .gitignore
echo "*.log" >> .gitignore

# Commit your archive
git commit -m "Initial archive setup"

# After writing sessions
git add exports/*.json
git commit -m "Update: Added chapter 5 to The Last Archive"
git push
```

### Collaborating with Others

1. **Export** your data as `nexus-archive-backup.json`
2. **Share** the backup file with collaborators
3. **They import** it into their Nexus Archive
4. **Merge changes** by exporting individual files and combining

---

## Manual JSON Editing

You can edit JSON files directly in any text editor!

### Example: Adding a Novel Manually

1. Export `novels.json`
2. Open in VS Code, Sublime Text, or any editor
3. Add a new entry:

```json
{
  "id": "id_1705312200000_new",
  "title": "My New Novel",
  "author": "Your Name",
  "genre": "Fantasy",
  "status": "draft",
  "description": "An amazing story...",
  "tags": "fantasy, adventure, magic",
  "createdAt": "2026-01-15T10:00:00.000Z",
  "updatedAt": "2026-01-15T10:00:00.000Z"
}
```

4. **Save** the file
5. **Import** it back into Nexus Archive

### ⚠️ JSON Editing Rules

- **Commas:** Every item except the last needs a comma
- **Quotes:** All keys and string values need double quotes
- **Brackets:** Arrays use `[]`, objects use `{}`
- **Validate:** Use a JSON validator before importing

**Recommended Tools:**
- [JSONLint](https://jsonlint.com/) - Online validator
- VS Code with Prettier extension
- [JSON Editor Online](https://jsoneditoronline.org/)

---

## Data Recovery

### If You Accidentally Delete Data

1. **Check your exports folder** for recent JSON files
2. **Import** the backup file
3. **Done!** Your data is restored

### If Browser Data is Cleared

1. **Open** Nexus Archive
2. **Import** your last backup (`nexus-archive-backup.json`)
3. **All data restored** from JSON files

### If Files are Corrupted

1. **Check** for previous dated backups
2. **Import** the most recent valid backup
3. **Validate** JSON files before importing

---

## Advanced Usage

### Syncing Across Devices

**Option 1: Cloud Storage**
1. Store JSON files in Google Drive / Dropbox / OneDrive
2. Export after each session
3. Import on other devices

**Option 2: Git Repository**
1. Push JSON files to GitHub/GitLab
2. Pull on other devices
3. Import the backup file

**Option 3: Manual Transfer**
1. Export all files
2. Transfer via USB/email/messaging
3. Import on target device

### Automated Backups (Advanced)

Create a script to automatically backup your exports folder:

**Windows (PowerShell):**
```powershell
$date = Get-Date -Format "yyyy-MM-dd"
Copy-Item "exports\*" "backups\archive-$date\" -Recurse
```

**Mac/Linux (Bash):**
```bash
#!/bin/bash
DATE=$(date +%Y-%m-%d)
mkdir -p backups/archive-$DATE
cp exports/* backups/archive-$DATE/
```

### Merging Multiple Archives

If you have data in multiple JSON files:

1. **Import** the main archive
2. **Import** additional files one by one
3. **Resolve conflicts** manually if IDs overlap
4. **Export** merged backup

---

## Troubleshooting

### "Invalid JSON" Error

**Cause:** The file has syntax errors

**Solution:**
1. Open file in a JSON validator
2. Fix any highlighted errors
3. Save and re-import

### "No Data Imported"

**Cause:** Wrong file format or empty file

**Solution:**
1. Check file contains valid data
2. Ensure you're importing to the correct type
3. Try importing the full backup instead

### Data Not Persisting

**Cause:** Browser localStorage cleared or disabled

**Solution:**
1. Enable localStorage in browser settings
2. Import your JSON backup
3. Export immediately to create fresh backup

### Chapters Not Showing

**Cause:** Chapters are linked to novels by `novelId`

**Solution:**
1. Ensure the parent novel exists
2. Check that `novelId` in chapters matches novel `id`
3. Import novels first, then chapters

---

## Best Practices

### ✅ Do

- Export after every writing session
- Keep dated backups weekly
- Store backups in multiple locations (cloud + local)
- Validate JSON before manual edits
- Use meaningful file names with dates

### ❌ Don't

- Rely only on browser localStorage
- Edit JSON without validating
- Delete old backups immediately
- Share backup files publicly (they contain your work!)

---

## File Size Limits

- **localStorage:** ~5-10MB depending on browser
- **JSON files:** No practical limit (tested up to 50MB)
- **Recommendation:** Export when approaching 3MB

### If Your Archive Gets Too Large

1. **Export** individual file types separately
2. **Archive** old novels to separate backup
3. **Clear** old data from active archive
4. **Import** archived data when needed

---

## Security Notes

⚠️ **Your JSON files contain your creative work!**

- **Encrypt** sensitive backups
- **Don't share** backup files publicly
- **Use strong passwords** if storing in cloud
- **Keep offline copies** for important work

---

## Support

For issues or questions:
1. Check the console for error messages (F12)
2. Validate your JSON files
3. Try importing individual files instead of full backup
4. Create a new archive and import data gradually

---

**Happy Writing! 🚀**

*The Nexus Archive Team*
