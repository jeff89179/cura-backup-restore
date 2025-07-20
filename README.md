# Cura Backup & Restore Script

This repository contains `cura_backup_restore.sh`, a self-contained Bash script for managing Ultimaker Cura configuration data on Linux systems.

## Features

- Backup all user-specific Cura configuration, plugin, and cache directories
- Restore from a previously generated backup file
- Clear all Cura config data (interactive mode only)
- Display all relevant Cura config paths (interactive mode only)
- Designed to support Cura AppImage-based installations
- Suitable for use in cronjobs or manual administration

## Included Paths

The script targets the following directories for backup, restore, and cleanup:

- `~/.config/cura/` – Cura settings, printers, profiles
- `~/.local/share/cura/` – User-installed plugins
- `~/.cache/cura/` – Cura cache packages
- `~/.cache/Ultimaker B.V./UltiMaker-Cura/` – Qt-related AppImage cache

All paths are user-scoped and resolved relative to `$HOME` for portability.

## Usage

### CLI Mode (for automation or cron)

#### Backup
```
./cura_backup_restore.sh --backup
```
- Creates a compressed .tar.gz backup archive in the user’s home directory.

#### Restore
```
./cura_backup_restore.sh --restore /path/to/backup_file.tar.gz
```
- Automatically backs up current Cura data before restoring
- Clear Clears existing Cura directories prior to extraction

#### Interactive Menu Mode
Run without any arguments:
```
./cura_backup_restore.sh
```
Available menu options:
- Backup Cura config
- Restore from a backup
- Clear all Cura config directories
- Show all config paths
- Exit

The interactive mode is the only way to access destructive actions like full config cleanup.

#### Installation (Optional)
To make the script globally accessible:

```
chmod +x cura_backup_restore.sh
sudo mv cura_backup_restore.sh /usr/local/bin/cura-backup
```
Then run it from anywhere with:
```
cura-backup
```
#### Requirements

- Bash (tested with Bash 5+)
- Standard GNU utilities (tar, rm, read, etc.)
- Linux environment (tested on Ubuntu 20.04+)

#### Example Cron Entry
Automated daily backup at 2:00 AM:
```
0 2 * * * /home/youruser/scripts/cura_backup_restore.sh --backup
```

#### Limitations
Only supports Linux. macOS and Windows are not supported at this time.

Restores overwrite existing Cura configuration.

No support for partial restores—it's all or nothing.

#### License
This project is licensed under the MIT License. See LICENSE for details.
