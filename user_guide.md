# 📚 File Organizer - Complete User Guide

Welcome to the comprehensive user guide for the File Organizer automation script! This guide will walk you through everything you need to know, from basic usage to advanced features.

---

## 📑 Table of Contents

1. [Getting Started](#getting-started)
2. [Step-by-Step Tutorial](#step-by-step-tutorial)
3. [Understanding File Categories](#understanding-file-categories)
4. [Advanced Usage](#advanced-usage)
5. [Configuration Deep Dive](#configuration-deep-dive)
6. [Best Practices](#best-practices)
7. [Real-World Use Cases](#real-world-use-cases)
8. [Command Reference Table](#command-reference-table)
9. [FAQ](#faq)
10. [Troubleshooting Guide](#troubleshooting-guide)

---

## 🚀 Getting Started

### What is File Organizer?

File Organizer is an intelligent Python script that automatically sorts your files into categorized folders based on their file type. It's like having a personal assistant that keeps your digital workspace tidy!

### Who Should Use This?

- 👨‍💼 **Professionals** - Keep your work folders organized
- 👨‍🎓 **Students** - Manage study materials efficiently
- 📸 **Photographers** - Sort media files quickly
- 💻 **Developers** - Organize project files
- 🏠 **Home Users** - Clean up personal files

### System Requirements

- **Operating System:** Windows 7+, macOS 10.12+, or Linux
- **Python Version:** 3.7 or higher
- **Disk Space:** 50MB for installation
- **RAM:** 100MB minimum

---

## 📖 Step-by-Step Tutorial

### Tutorial 1: Your First Organization

Let's organize your Downloads folder step-by-step.

#### Step 1: Open Terminal/Command Prompt

**Windows:**
- Press `Win + R`
- Type `cmd` and press Enter

**Mac/Linux:**
- Press `Cmd + Space` (Mac) or `Ctrl + Alt + T` (Linux)
- Type `terminal` and press Enter

#### Step 2: Navigate to Script Location

```bash
# Change to the directory where file_organizer.py is located
cd /path/to/file-organizer

# Example:
cd C:\Users\YourName\Documents\file-organizer    # Windows
cd ~/Documents/file-organizer                     # Mac/Linux
```

#### Step 3: Run a Dry Run First (Recommended)

```bash
python file_organizer.py -p ~/Downloads --dry-run
```

**What Happens:**
- Script scans all files in Downloads
- Shows what changes would be made
- **No files are actually moved**
- You see a preview of the organization

**Expected Output:**
```
╔═══════════════════════════════════════════════════════════╗
║            Intelligent File Organization System           ║
╚═══════════════════════════════════════════════════════════╝

🔍 DRY RUN MODE - No files will be moved

Found 45 file(s) to organize.
Organizing files... ████████████████████ 100%

📊 Organization Summary
┏━━━━━━━━━━━━━┳━━━━━━━┓
┃ Metric      ┃ Value ┃
┡━━━━━━━━━━━━━╇━━━━━━━┩
│ Total Files │ 45    │
│ Organized   │ 45    │
│ Skipped     │ 0     │
│ Errors      │ 0     │
│ Time Taken  │ 0.23s │
└─────────────┴───────┘

📁 Files by Category
┏━━━━━━━━━━━┳━━━━━━━┓
┃ Category  ┃ Count ┃
┡━━━━━━━━━━━╇━━━━━━━┩
│ Documents │ 15    │
│ Images    │ 12    │
│ Videos    │ 8     │
│ Archives  │ 10    │
└───────────┴───────┘
```

#### Step 4: Perform Actual Organization

If the preview looks good:

```bash
python file_organizer.py -p ~/Downloads
```

✅ **Success!** Your files are now organized into categories.

#### Step 5: Verify the Results

Navigate to your Downloads folder and you'll see:

```
Downloads/
├── Documents/
│   ├── report.pdf
│   ├── resume.docx
│   └── budget.xlsx
├── Images/
│   ├── photo1.jpg
│   └── screenshot.png
├── Videos/
│   └── tutorial.mp4
└── Archives/
    └── backup.zip
```

#### Step 6: Undo If Needed

Made a mistake? No problem!

```bash
python file_organizer.py -p ~/Downloads --undo
```

All files return to their original locations.

---

### Tutorial 2: Creating Custom Categories

Want to add your own file categories? Here's how:

#### Step 1: Create Configuration File

```bash
python file_organizer.py --create-config
```

This creates a `config.json` file in your current directory.

#### Step 2: Edit the Configuration

Open `config.json` in any text editor and add your categories:

```json
{
  "categories": {
    "Documents": [".pdf", ".docx", ".txt"],
    "Images": [".jpg", ".png", ".gif"],
    "3D Models": [".obj", ".fbx", ".blend", ".stl"],
    "eBooks": [".epub", ".mobi", ".azw3"],
    "Spreadsheets": [".xlsx", ".xls", ".csv"]
  }
}
```

#### Step 3: Use Custom Config

```bash
python file_organizer.py -p ~/Downloads -c config.json
```

Now your files will be organized using your custom categories!

---

### Tutorial 3: Recursive Organization

Organize files in subdirectories too:

#### Example Folder Structure:
```
Projects/
├── file1.py
├── Subfolder1/
│   ├── image.png
│   └── document.pdf
└── Subfolder2/
    └── video.mp4
```

#### Command:
```bash
python file_organizer.py -p ~/Projects -r
```

#### Result:
```
Projects/
├── Code/
│   └── file1.py
├── Images/
│   └── image.png
├── Documents/
│   └── document.pdf
└── Videos/
    └── video.mp4
```

All files from subdirectories are organized at the root level.

---

## 📂 Understanding File Categories

### Default Categories

| Category | File Types | Extensions |
|----------|-----------|------------|
| **Documents** | Text documents, PDFs, Office files | .pdf, .doc, .docx, .txt, .xlsx, .ppt |
| **Images** | Photos, graphics, icons | .jpg, .png, .gif, .svg, .bmp, .webp |
| **Videos** | Video files | .mp4, .avi, .mkv, .mov, .wmv |
| **Audio** | Music, podcasts, sound files | .mp3, .wav, .flac, .aac, .ogg |
| **Archives** | Compressed files | .zip, .rar, .7z, .tar, .gz |
| **Code** | Programming files | .py, .js, .java, .cpp, .html, .css |
| **Executables** | Installable programs | .exe, .msi, .app, .deb, .apk |
| **Others** | Everything else | (any unlisted extension) |

### How Categorization Works

1. **Extension Detection:** Script reads the file extension (e.g., `.pdf`)
2. **Category Lookup:** Searches config for matching category
3. **Folder Creation:** Creates category folder if it doesn't exist
4. **File Movement:** Moves file to appropriate category folder

### Files Without Extensions

Files without extensions (e.g., `README`, `Makefile`) are automatically placed in the **Others** category.

---

## 🎓 Advanced Usage

### Combining Multiple Options

```bash
# Dry run + Verbose + Recursive
python file_organizer.py -p ~/Documents -d -v -r

# Custom config + Quiet mode
python file_organizer.py -p ~/Files -c my_config.json -q

# Recursive + Verbose (detailed organization)
python file_organizer.py -p ~/Projects -r -v
```

### Automation with Cron Jobs (Linux/Mac)

Organize your Downloads folder automatically every day:

```bash
# Edit crontab
crontab -e

# Add this line (runs daily at 2 AM)
0 2 * * * /usr/bin/python3 /path/to/file_organizer.py -p ~/Downloads -q

# Or weekly on Sundays at midnight
0 0 * * 0 /usr/bin/python3 /path/to/file_organizer.py -p ~/Downloads -q
```

### Automation with Task Scheduler (Windows)

1. Open Task Scheduler
2. Create Basic Task
3. Name: "Organize Downloads"
4. Trigger: Daily at 2:00 AM
5. Action: Start a Program
   - Program: `python.exe`
   - Arguments: `file_organizer.py -p C:\Users\YourName\Downloads -q`
   - Start in: `C:\path\to\script\`

### Batch Processing Multiple Folders

Create a shell script to organize multiple directories:

**Linux/Mac (organize_all.sh):**
```bash
#!/bin/bash

python file_organizer.py -p ~/Downloads -q
python file_organizer.py -p ~/Desktop -q
python file_organizer.py -p ~/Documents -q

echo "All folders organized!"
```

**Windows (organize_all.bat):**
```batch
@echo off
python file_organizer.py -p C:\Users\%USERNAME%\Downloads -q
python file_organizer.py -p C:\Users\%USERNAME%\Desktop -q
python file_organizer.py -p C:\Users\%USERNAME%\Documents -q

echo All folders organized!
pause
```

---

## ⚙️ Configuration Deep Dive

### Complete Configuration Example

```json
{
  "categories": {
    "Documents": [".pdf", ".docx", ".txt", ".rtf", ".odt"],
    "Images": [".jpg", ".png", ".gif", ".bmp", ".svg"],
    "Videos": [".mp4", ".avi", ".mkv", ".mov"],
    "Audio": [".mp3", ".wav", ".flac", ".aac"],
    "Archives": [".zip", ".rar", ".7z", ".tar"],
    "Code": [".py", ".js", ".html", ".css", ".java"],
    "3D_Models": [".obj", ".fbx", ".blend", ".stl"],
    "eBooks": [".epub", ".mobi", ".azw3", ".pdf"],
    "Fonts": [".ttf", ".otf", ".woff", ".woff2"],
    "Databases": [".db", ".sqlite", ".sql", ".mdb"],
    "Others": []
  },
  "ignore_files": [
    ".ds_store",
    "thumbs.db",
    "desktop.ini",
    ".gitignore",
    "README.md"
  ],
  "ignore_folders": [
    "node_modules",
    ".git",
    "__pycache__",
    "venv",
    ".vscode",
    "Documents",
    "Images",
    "Videos"
  ],
  "duplicate_strategy": "rename",
  "log_file": "file_organizer.log",
  "log_level": "INFO",
  "max_log_size": 5242880,
  "backup_count": 3
}
```

### Configuration Options Explained

#### 1. Categories
Define custom file type groupings:

```json
"categories": {
  "MyCategory": [".ext1", ".ext2", ".ext3"]
}
```

**Tips:**
- Use descriptive category names
- Extensions must include the dot (`.`)
- Extensions are case-insensitive
- Can have same extension in multiple categories (first match wins)

#### 2. Ignore Files
Files to skip during organization:

```json
"ignore_files": [".ds_store", "thumbs.db", "desktop.ini"]
```

**Common additions:**
- `.gitignore`
- `README.md`
- `.env`
- `config.ini`

#### 3. Ignore Folders
Directories to skip:

```json
"ignore_folders": ["node_modules", ".git", "__pycache__"]
```

**Important:** Category folders are automatically added to ignore list.

#### 4. Duplicate Strategy

**Options:**

```json
"duplicate_strategy": "rename"  // Default
```

- **`rename`** - Adds timestamp: `file_20241015_143022.pdf`
- **`skip`** - Keeps original, skips new file
- **`overwrite`** - Replaces old with new (⚠️ Use carefully!)

#### 5. Logging Configuration

```json
"log_file": "file_organizer.log",
"log_level": "INFO",
"max_log_size": 5242880,  // 5MB
"backup_count": 3
```

**Log Levels:**
- `DEBUG` - Most detailed (development)
- `INFO` - General information (default)
- `WARNING` - Only warnings and errors
- `ERROR` - Only errors

---

## 💡 Best Practices

### 1. Always Test with Dry Run First

```bash
# GOOD: Test before organizing
python file_organizer.py -p ~/Important_Files --dry-run
python file_organizer.py -p ~/Important_Files

# RISKY: Organizing without testing
python file_organizer.py -p ~/Important_Files  # Skip this step!
```

### 2. Backup Important Data

Before organizing critical files:
```bash
# Create backup
cp -r ~/Important_Files ~/Important_Files_Backup

# Then organize
python file_organizer.py -p ~/Important_Files
```

### 3. Start Small

Don't organize your entire computer at once!

```bash
# ✅ GOOD: Start with one folder
python file_organizer.py -p ~/Downloads

# ❌ BAD: Organizing system folders
python file_organizer.py -p /  # Never do this!
```

### 4. Use Verbose Mode for Learning

```bash
# See exactly what's happening
python file_organizer.py -p ~/Test_Folder -v
```

### 5. Organize Regularly

Set up weekly organization:
- Downloads folder: Weekly
- Desktop: Bi-weekly
- Documents: Monthly

### 6. Customize for Your Workflow

Create different configs for different needs:
- `work_config.json` - Work files
- `personal_config.json` - Personal files
- `media_config.json` - Photos/videos

### 7. Check Logs Regularly

```bash
# View recent log entries
tail -n 50 file_organizer.log

# Search for errors
grep ERROR file_organizer.log
```

### 8. Don't Organize System Folders

**Never organize these:**
- `/System` (Mac)
- `C:\Windows` (Windows)
- `/usr`, `/bin`, `/etc` (Linux)
- User Library folders

**Safe to organize:**
- `~/Downloads`
- `~/Desktop`
- `~/Documents`
- `~/Pictures`
- Custom project folders

---

## 🌍 Real-World Use Cases

### Use Case 1: Student Organizing Study Materials

**Scenario:** Sarah has 200+ files scattered across her Downloads folder from a semester of online classes.

**Solution:**
```bash
# Custom config for student files
{
  "categories": {
    "Lectures": [".pdf", ".ppt", ".pptx"],
    "Assignments": [".doc", ".docx", ".txt"],
    "Videos": [".mp4", ".avi"],
    "Code": [".py", ".java", ".cpp"],
    "Research": [".pdf", ".epub"]
  }
}

# Organize
python file_organizer.py -p ~/Downloads -c student_config.json -v
```

**Result:** All study materials neatly organized by type!

### Use Case 2: Photographer Managing Photos

**Scenario:** John downloads 500 photos from various shoots.

**Custom Config:**
```json
{
  "categories": {
    "RAW_Photos": [".raw", ".cr2", ".nef", ".arw"],
    "Edited_JPG": [".jpg", ".jpeg"],
    "PNG_Graphics": [".png"],
    "Project_Files": [".psd", ".ai", ".xd"]
  }
}
```

### Use Case 3: Developer Cleaning Project Folder

**Scenario:** Mixed files in a project directory.

```bash
# Organize keeping source code structure
python file_organizer.py -p ~/MyProject -r -c dev_config.json
```

**Config focuses on:**
- Separating source code
- Organizing documentation
- Grouping assets

### Use Case 4: Home Office Cleanup

**Weekly automation:**
```bash
#!/bin/bash
# weekly_cleanup.sh

echo "Starting weekly file organization..."

python file_organizer.py -p ~/Downloads -q
python file_organizer.py -p ~/Desktop -q

echo "Weekly cleanup complete!"
```

### Use Case 5: Archive Preparation

Before backing up:
```bash
# Organize everything
python file_organizer.py -p ~/Archive_2024 -r -v

# Review organization
ls -R ~/Archive_2024

# Then backup
tar -czf archive_2024.tar.gz ~/Archive_2024
```

---

## 📊 Command Reference Table

| Command | Short | Arguments | Description | Example |
|---------|-------|-----------|-------------|---------|
| `--path` | `-p` | Directory path | Target folder to organize | `-p ~/Downloads` |
| `--config` | `-c` | Config file path | Custom configuration | `-c my_config.json` |
| `--dry-run` | `-d` | None | Preview without moving | `-d` |
| `--undo` | `-u` | None | Reverse last operation | `-u` |
| `--recursive` | `-r` | None | Include subdirectories | `-r` |
| `--verbose` | `-v` | None | Detailed output | `-v` |
| `--quiet` | `-q` | None | Minimal output | `-q` |
| `--create-config` | - | None | Generate default config | `--create-config` |
| `--version` | - | None | Show version | `--version` |
| `--help` | `-h` | None | Display help | `-h` |

### Common Command Combinations

```bash
# Preview with details
python file_organizer.py -p ~/folder -d -v

# Silent organization for automation
python file_organizer.py -p ~/folder -q

# Deep organization with custom settings
python file_organizer.py -p ~/folder -r -c config.json -v

# Quick undo
python file_organizer.py -p ~/folder -u
```

---

## ❓ FAQ (Frequently Asked Questions)

### General Questions

**Q1: Is this safe to use?**
> Yes! The script has built-in safety features:
> - Dry-run mode for testing
> - Undo functionality
> - Never overwrites by default
> - Comprehensive logging

**Q2: Will it delete my files?**
> No! The script only moves files, never deletes them.

**Q3: Can I organize multiple folders at once?**
> Not directly, but you can create a script:
> ```bash
> python file_organizer.py -p ~/folder1 -q
> python file_organizer.py -p ~/folder2 -q
> ```

**Q4: Does it work on external drives?**
> Yes! Just provide the external drive path:
> ```bash
> python file_organizer.py -p /Volumes/MyDrive  # Mac
> python file_organizer.py -p E:\MyDrive        # Windows
> ```

**Q5: What happens to files without extensions?**
> They go into the "Others" category.

### Technical Questions

**Q6: How do I organize only specific file types?**
> Create a custom config with only those types:
> ```json
> {
>   "categories": {
>     "Images_Only": [".jpg", ".png", ".gif"]
>   }
> }
> ```

**Q7: Can I organize by date instead of type?**
> Not directly, but you can modify the script or organize first, then use other tools.

**Q8: How much disk space do I need?**
> The same as your files occupy. Organization doesn't compress or change file sizes.

**Q9: Will it work with network drives?**
> Yes, but performance may be slower due to network speed.

**Q10: Can I pause and resume organization?**
> Press `Ctrl+C` to stop. Run again to continue with remaining files.

### Troubleshooting Questions

**Q11: Why are some files not being organized?**
> Check:
> - File extension is in config.json
> - File isn't in ignore_files list
> - You have read/write permissions

**Q12: How do I see what went wrong?**
> Check the log file:
> ```bash
> cat file_organizer.log | grep ERROR
> ```

**Q13: Undo isn't working. What should I do?**
> The history file may be deleted. Check for `.file_organizer_history.json` in the organized folder.

**Q14: Can I organize files larger than 4GB?**
> Yes! The script handles files of any size (limited by your disk space).

**Q15: It says "Permission Denied." What now?**
> Run with elevated permissions:
> ```bash
> sudo python file_organizer.py -p ~/folder  # Mac/Linux
> ```
> Or change folder permissions first.

---

## 🔧 Troubleshooting Guide

### Issue 1: Script Won't Start

**Symptoms:**
```
python: command not found
```

**Solutions:**
```bash
# Try python3 instead
python3 file_organizer.py -p ~/folder

# Check Python installation
which python
python --version

# Install Python if missing
# Mac: brew install python3
# Ubuntu: sudo apt install python3
# Windows: Download from python.org
```

### Issue 2: Missing Dependencies

**Symptoms:**
```
ModuleNotFoundError: No module named 'rich'
```

**Solutions:**
```bash
# Install dependencies
pip install -r requirements.txt

# Or install individually
pip install rich

# If pip doesn't work, try pip3
pip3 install rich
```

### Issue 3: Permission Errors

**Symptoms:**
```
PermissionError: [Errno 13] Permission denied
```

**Solutions:**
```bash
# Check folder permissions
ls -la ~/folder

# Change permissions (Linux/Mac)
chmod -R u+w ~/folder

# Run with sudo (use carefully)
sudo python file_organizer.py -p ~/folder

# On Windows, run Command Prompt as Administrator
```

### Issue 4: Files Not Moving

**Symptoms:**
- Script runs but files stay in place
- No error messages

**Checklist:**
- [ ] Are you in dry-run mode? (Remove `--dry-run`)
- [ ] Check if extensions are in config.json
- [ ] Look for errors in log file
- [ ] Verify you have write permissions
- [ ] Check if files are in ignore list

### Issue 5: Slow Performance

**Symptoms:**
- Script takes a long time
- High CPU/memory usage

**Solutions:**
```bash
# Disable verbose mode
python file_organizer.py -p ~/folder -q

# Don't use recursive on large directories
# Organize subdirectories individually

# Close other programs
# Ensure enough free disk space (20% minimum)
```

### Issue 6: Duplicate Handling Issues

**Symptoms:**
- Files being skipped unexpectedly
- Duplicate names with timestamps

**Solutions:**
```json
// Change duplicate strategy in config.json
{
  "duplicate_strategy": "rename"  // or "skip" or "overwrite"
}
```

### Issue 7: Undo Not Working

**Symptoms:**
```
No history found. Nothing to undo.
```

**Solutions:**
- Check if `.file_organizer_history.json` exists
- Undo only works for most recent operation
- If file is deleted, restore from backup
- Run organization again to create new history

### Issue 8: Config File Errors

**Symptoms:**
```
ConfigError: Invalid JSON in config file
```

**Solutions:**
- Validate JSON at jsonlint.com
- Check for missing commas, brackets
- Remove comments (JSON doesn't support comments)
- Regenerate default config:
  ```bash
  python file_organizer.py --create-config
  ```

### Issue 9: Unicode/Special Characters

**Symptoms:**
- Files with special characters fail to move
- Error messages with garbled text

**Solutions:**
```bash
# Ensure UTF-8 encoding
export LANG=en_US.UTF-8  # Linux/Mac

# Rename problematic files first
# Or add to ignore list
```

### Issue 10: Network Drive Issues

**Symptoms:**
- Very slow performance on network drives
- Intermittent failures

**Solutions:**
- Ensure stable network connection
- Copy files locally first, then organize
- Increase timeout in script (advanced)
- Use wired connection instead of Wi-Fi

---

## 📈 Performance Tips

### 1. Optimize for Speed

```bash
# Use quiet mode (faster)
python file_organizer.py -p ~/folder -q

# Avoid recursive on large directories
# Process subdirectories individually
```

### 2. Reduce Log Size

```json
{
  "log_level": "WARNING",  // Less detailed logging
  "max_log_size": 1048576  // 1MB instead of 5MB
}
```

### 3. Exclude Unnecessary Files

```json
{
  "ignore_files": [
    ".ds_store",
    "thumbs.db",
    "*.tmp",
    "*.cache"
  ]
}
```

### 4. Batch Processing

Instead of organizing 10,000 files at once:
```bash
# Organize in smaller batches
python file_organizer.py -p ~/folder/batch1
python file_organizer.py -p ~/folder/batch2
```

---

## 🎓 Learning Path

### Beginner Level (Week 1-2)
1. Install and setup
2. Practice with dry-run mode
3. Organize Downloads folder
4. Learn undo functionality
5. Review log files

### Intermediate Level (Week 3)
1. Create custom configurations
2. Add new categories
3. Set up automation (cron/task scheduler)
4. Use recursive mode
5. Handle edge cases

### Advanced Level (Week 4)
1. Modify script for custom needs
2. Create batch processing scripts
3. Integrate with other tools
4. Optimize performance
5. Contribute improvements

---

## 📞 Getting Help

### Before Asking for Help

1. ✅ Check this user guide
2. ✅ Review the log file
3. ✅ Try with `--verbose` mode
4. ✅ Search existing issues on GitHub
5. ✅ Try with a small test folder first

### Where to Get Help

1. **GitHub Issues**: Report bugs or request features
2. **Documentation**: README.md and this guide
3. **Log Files**: Most answers are in the logs
4. **Community**: Stack Overflow, Reddit r/Python

### How to Report Issues

Include this information:
```
- Operating System: (e.g., Windows 10, macOS 13, Ubuntu 22.04)
- Python Version: (run `python --version`)
- Script Version: 1.0.0
- Command Used: (e.g., `python file_organizer.py -p ~/test`)
- Error Message: (full error from terminal)
- Log File: (last 20 lines of file_organizer.log)
```

---

## 🎯 Quick Reference Card

### Most Common Commands
```bash
# Basic organize
python file_organizer.py -p ~/Downloads

# Preview first
python file_organizer.py -p ~/Downloads --dry-run

# Undo
python file_organizer.py -p ~/Downloads --undo

# With details
python file_organizer.py -p ~/Downloads -v

# Include subfolders
python file_organizer.py -p ~/Projects -r
```

### Quick Troubleshooting
```bash
# Check version
python file_organizer.py --version

# View help
python file_organizer.py --help

# Check logs
tail -f file_organizer.log

# Test configuration
python file_organizer.py --create-config
```

---

## 📝 Cheat Sheet

| Task | Command |
|------|---------|
| Organize folder | `python file_organizer.py -p /path` |
| Test first | Add `--dry-run` |
| See details | Add `-v` |
| Silent mode | Add `-q` |
| Include subfolders | Add `-r` |
| Undo changes | Add `--undo` |
| Custom config | Add `-c config.json` |
| Create config | `--create-config` |
| View help | `--help` or `-h` |
| Check version | `--version` |

---

## 🚀 Next Steps

Now that you've completed this guide:

1. ✅ Practice with test folders
2. ✅ Create your custom configurations
3. ✅ Set up automation for regular organization
4. ✅ Share your success with others
5. ✅ Contribute improvements to the project

---

## 💬 Feedback

Found this guide helpful? Have suggestions for improvement?

- ⭐ Star the project on GitHub
- 📝 Open an issue for corrections
- 🔄 Submit a pull request for additions
- 📧 Email feedback to: your.email@example.com

---

**Happy Organizing! 🎉**

*Last Updated: October 2024*
*Version: 1.0.0*