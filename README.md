[简体中文](README_zh.md)

# Git Index Reader - git-read-index

## Overview
`git-read-index` is a Python utility tool that reads and parses Git index files (`.git/index`) to display detailed information about staged files in a Git repository. This tool provides insights into the staging area contents, including file metadata, permissions, SHA-1 checksums, and more.

## Features
* **Native Parsing**: Parses Git index files directly without relying on external Git commands.
* **Detailed Information**: Displays granular details for each staged file, including mode (permissions), size, and modification time (mtime).
* **Integrity Verification**: Automatically validates SHA-1 checksums to ensure the integrity of the index file.
* **Extension Support**: Capable of parsing various Git index extensions.
* **User-Friendly Output**: Features color-coded console output for enhanced readability and automatic detection of the Git repository location.

## Prerequisites
* Python 3.x
* Git installed and configured on your system
* A Git repository to analyze (the tool works within any valid Git directory)

## Installation

### Direct Download
Download the `git-read-index` script from this repository and make it executable:
```bash
chmod +x git-read-index
cp git-read-index /path/to/your/executables/
```

## Usage

### Basic Usage
Run the script from within any Git repository:
```bash
./git-read-index
# or
python3 git-read-index
```

### Command Line Options
The script automatically detects the Git repository in the current or parent directories. No additional arguments are required for standard operations.

### Output Format Example
The tool presents information in a structured, easy-to-read format:

```text
============================================================
[ Git Index Header ]
  Magic Number  : 4D5F5347
  Version       : 2
  Entries Count : 15
============================================================
[ Staging Entries ]
------------------------------------------------------------
 [1] src/main.py
     └─ Mode (Permissions) : 100644
     └─ File Size          : 1024 bytes
     └─ Blob SHA-1         : a1b2c3d4e5f67890123456789012345678901234
     └─ Modified (mtime)   : 1634567890
------------------------------------------------------------
[ Extensions ]
  Found Extension: TREE (Size: 20 bytes)
  Found Extension: REUC (Size: 12 bytes)
============================================================
```

## Examples

**View Current Repository Index:**
```bash
cd /path/to/your/git/repo
./git-read-index
```

**Check Index Integrity:**
The tool automatically validates SHA-1 checksums and will issue a warning if corruption is detected:
```text
⚠️ WARNING: Index file SHA-1 checksum failed, file may be corrupted!
```

## Troubleshooting

| Issue | Cause | Solution |
| :--- | :--- | :--- |
| `FATAL ERROR: Not in Git Repository` | The current or parent directory is not a Git repository. | Run the script from within a valid Git project directory. |
| `Permission denied` | The script lacks execution permissions. | Execute `chmod +x git-read-index`. |
| `SHA-1 checksum failed` | The index file might be corrupted or tampered with. | Run `git status` to check repository integrity; use `git reset` if necessary. |

## Debugging Tips
* **Verify Git Installation**:
  ```bash
  git --version
  ```
* **Check Git Repository Structure**:
  ```bash
  ls -la .git/
  ```
* **Validate Index File Location**:
  ```bash
  git rev-parse --git-dir
  ```

## Contributing
Contributions are welcome! Please feel free to submit a Pull Request.
