# Task 7 — Analyze, Verify & Manage Backup

## Objective

Analyze the APP01 backup, verify the restore point, scan the backup for malware, and review the retention configuration.

## Backup Verification

The `APP01-Backup` job was checked after the first successful backup.

- Backup Job: `APP01-Backup`
- Computer: `APP01`
- Backup Type: Windows Agent Backup
- Restore Points: 1
- Repository: `VEEAM01-Repository`
- Last Result: Success
- Errors: 0
- Warnings: 0

The backup was stored in:

    D:\VeeamRepository\APP01-Backup\10.10.20.4\

## Backup Scan

Veeam `Scan Backup` was used with **Veeam Threat Hunter** to scan the restore point for malware.

Configuration:

- Scan Mode: Find the last clean restore point
- Scan Engine: Veeam Threat Hunter
- YARA: Disabled

The first scan attempt was canceled by the user.

The second scan completed successfully.

### Final Scan Result

- Status: Success
- APP01 Scan: Success
- Malware Scan Test: Success

The `FLR_[app01]` session shown during the scan was an internal session created by the backup scanning process. It was not the File-Level Restore task.

## Retention Management

The `APP01-Backup` job retention configuration was reviewed.

- Retention: **7 days**
- Repository: `VEEAM01-Repository`
- Repository Capacity: **100 GB**
- Available Space: **86.8 GB**
- GFS Retention: Disabled
- Secondary Backup Destination: Disabled

The current retention configuration is suitable for this lab.

Retention management controls how long backup restore points are kept and helps prevent unnecessary use of repository storage.

## Result

The APP01 backup was successfully analyzed and verified.

- Backup exists: Yes
- Restore Point available: Yes
- Malware Scan: Success
- Retention configured: 7 days
- Backup Job: Success
- Errors: 0
- Warnings: 0

## Status
<img width="1674" height="932" alt="image" src="https://github.com/user-attachments/assets/02b2f943-3f39-41ba-8502-359772f617c7" />

**Completed**

