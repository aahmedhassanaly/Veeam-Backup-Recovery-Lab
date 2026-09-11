# Task 8 — File-Level Restore

## Objective

Restore a deleted file from a Veeam backup and verify that the recovery was successful.

## Scenario

A test file was created on `APP01`:

    C:\VeeamLab\test.txt

A new backup of `APP01` was then completed successfully.

After the backup finished, the file was deleted from `APP01` to simulate accidental file deletion.

## Restore Process

The backup was opened using:

**Backups → Disk → APP01-Backup → Restore guest files → Microsoft Windows**

Veeam opened the **Backup Browser**, which allowed access to the files stored inside the restore point.

The following file was located:

    C:\VeeamLab\test.txt

The file was restored using **Restore to...**

The restore operation completed successfully and the file was available again on the system.

## Result

The File-Level Restore was successful.

The recovery workflow was:

    Create File
    ↓
    Backup
    ↓
    Delete File
    ↓
    Open Backup Browser
    ↓
    Restore Guest File
    ↓
    Verify File

This confirms that individual files can be recovered without restoring the entire computer.

## Important Concepts

### Restore to Original Location

Restores the selected file back to its original path.

Example:

    C:\VeeamLab\test.txt

### Restore to Another Location

Restores the file to a different path or location.

This is useful when the original location is unavailable or when the administrator wants to inspect the recovered file before replacing the original.

### Keep / Overwrite

When a file with the same name already exists in the destination:

- **Keep** — keeps the existing file.
- **Overwrite** — replaces the existing file with the restored version.

## Real-World Use

File-Level Restore is commonly used for:

- Accidentally deleted files
- Overwritten files
- Recovering previous file versions
- Restoring user data without restoring the whole server

## Status
<img width="1297" height="777" alt="image" src="https://github.com/user-attachments/assets/c5a1d07b-a051-4909-b39c-40c49df09b92" />

**Completed**
