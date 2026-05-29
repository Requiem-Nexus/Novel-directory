# Nexus Archive - JSON File Structure

## Overview

Nexus Archive saves your data in separate JSON files for easy backup, version control, and portability. Each data type is stored in its own file.

## File Structure

```
nexus-archive/
├── index.html              # Main application
├── novels.json             # All novel data
├── characters.json         # All character data
├── lore.json               # All lore entries
├── chapters.json           # All chapter data
├── settings.json           # User preferences
└── nexus-archive-backup.json  # Complete backup (all data)
```

---

## JSON File Formats

### novels.json

Array of novel objects:

```json
[
  {
    "id": "id_1234567890_abc123",
    "title": "The Last Archive",
    "author": "A.I. Writer",
    "genre": "Sci-Fi",
    "status": "draft",
    "description": "In a world where knowledge is power...",
    "tags": "sci-fi, dystopian, archive, future",
    "createdAt": "2026-01-15T10:30:00.000Z",
    "updatedAt": "2026-01-15T12:45:00.000Z"
  }
]
```

**Fields:**
- `id` - Unique identifier (auto-generated)
- `title` - Novel title (required)
- `author` - Author name
- `genre` - Genre category (Fantasy, Sci-Fi, Romance, Mystery, Horror, Thriller, Adventure, Other)
- `status` - "draft" or "published"
- `description` - Novel synopsis
- `tags` - Comma-separated tags
- `createdAt` - ISO 8601 timestamp
- `updatedAt` - ISO 8601 timestamp

---

### characters.json

Array of character objects:

```json
[
  {
    "id": "id_1234567890_def456",
    "name": "Dr. Elena Vance",
    "role": "Protagonist",
    "affiliation": "Nexus Archive",
    "power": 75,
    "novelId": "id_1234567890_abc123",
    "description": "Chief archivist and protector...",
    "createdAt": "2026-01-15T10:30:00.000Z",
    "updatedAt": "2026-01-15T12:45:00.000Z"
  }
]
```

**Fields:**
- `id` - Unique identifier (auto-generated)
- `name` - Character name (required)
- `role` - Character role (Protagonist, Antagonist, Supporting, etc.)
- `affiliation` - Organization or group
- `power` - Power level (1-100)
- `novelId` - Reference to parent novel
- `description` - Character background
- `createdAt` - ISO 8601 timestamp
- `updatedAt` - ISO 8601 timestamp

---

### lore.json

Array of lore entry objects:

```json
[
  {
    "id": "id_1234567890_ghi789",
    "title": "The Great Collapse",
    "category": "History",
    "era": "Pre-Archive Era",
    "content": "The Great Collapse marked the end...",
    "novelId": "id_1234567890_abc123",
    "createdAt": "2026-01-15T10:30:00.000Z",
    "updatedAt": "2026-01-15T12:45:00.000Z"
  }
]
```

**Fields:**
- `id` - Unique identifier (auto-generated)
- `title` - Entry title (required)
- `category` - Category (History, World-Building, Magic System, Technology, Culture, Geography, Other)
- `era` - Timeline era or period
- `content` - Full lore content (required)
- `novelId` - Reference to related novel
- `createdAt` - ISO 8601 timestamp
- `updatedAt` - ISO 8601 timestamp

---

### chapters.json

Array of chapter collection objects (one per novel):

```json
[
  {
    "novelId": "id_1234567890_abc123",
    "chapters": [
      {
        "id": "id_1234567890_jkl012",
        "number": 1,
        "title": "The Beginning",
        "status": "published",
        "content": "It was a dark and stormy night...",
        "createdAt": "2026-01-15T10:30:00.000Z"
      }
    ]
  }
]
```

**Fields:**
- `novelId` - Reference to parent novel
- `chapters` - Array of chapter objects
  - `id` - Unique identifier (auto-generated)
  - `number` - Chapter number
  - `title` - Chapter title (required)
  - `status` - "draft" or "published"
  - `content` - Chapter content
  - `createdAt` - ISO 8601 timestamp

---

### settings.json

Single settings object:

```json
{
  "archiveName": "Nexus Archive",
  "autoExport": "manual"
}
```

**Fields:**
- `archiveName` - Custom archive name
- `autoExport` - "always" or "manual"

---

### nexus-archive-backup.json

Complete backup containing all data:

```json
{
  "exportDate": "2026-01-15T14:00:00.000Z",
  "version": "1.0",
  "archiveName": "Nexus Archive",
  "files": {
    "novels": [...],
    "characters": [...],
    "lore": [...],
    "chapters": [...],
    "settings": {...}
  }
}
```

---

## Usage Guide

### Exporting Data

1. **Individual Files:**
   - Go to Settings → JSON File Export
   - Click on any file button to download that specific JSON file

2. **All Files:**
   - Click "Download All JSON Files" to download all 5 files at once

3. **Full Backup:**
   - Data is automatically exported after saves (if enabled)
   - Creates a single `nexus-archive-backup.json` file

### Importing Data

1. **Individual Files:**
   - Go to Settings → JSON File Import
   - Click "Import [filename].json" button
   - Select the corresponding JSON file

2. **Full Backup:**
   - Click "Import Full Backup"
   - Select `nexus-archive-backup.json`
   - All data will be restored

### Version Control

You can use these JSON files with Git:

```bash
# Initialize git repo
git init

# Add JSON files
git add *.json

# Commit changes
git commit -m "Backup archive data"

# Push to remote
git push origin main
```

### Manual Editing

You can manually edit JSON files:

1. Export the file you want to edit
2. Open in any text editor or JSON editor
3. Make your changes (maintain the structure!)
4. Import the file back

**⚠️ Warning:** Invalid JSON will fail to import. Use a JSON validator.

---

## Data Sync Strategy

The application uses a hybrid approach:

1. **localStorage** - Primary storage for fast access
2. **JSON Files** - Backup and portability

**Auto-Export:** When enabled, JSON files are automatically downloaded after each save operation.

**Manual Export:** Always available in Settings for on-demand backups.

---

## Best Practices

1. **Regular Backups:** Export your JSON files weekly or after major changes
2. **Version Naming:** Add dates to backup files: `nexus-archive-2026-01-15.json`
3. **Cloud Storage:** Store JSON files in cloud storage (Google Drive, Dropbox, etc.)
4. **Git Repository:** Use Git for version control and history
5. **Validate Before Import:** Check JSON validity before importing edited files

---

## Troubleshooting

### Import Failed
- Check if the file is valid JSON
- Ensure the file structure matches the expected format
- Try importing individual files instead of full backup

### Data Not Persisting
- Check browser localStorage is enabled
- Clear browser cache and reload
- Export data before clearing browser data

### Missing Chapters
- Chapters are linked to novels by `novelId`
- Ensure the parent novel exists before importing chapters

---

## Support

For issues or questions about the JSON file format, refer to the application's Settings page or check the console for error messages.
