# Task 7 — Analyze and Verify Backup

## Objective

Analyze the APP01 backup and verify that the backup can be scanned successfully.

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

## Scan Backup

Veeam `Scan Backup` was used to check the restore point for malware.

Configuration:

- Scan Mode: Find the last clean restore point
- Scan Engine: Veeam Threat Hunter
- YARA: Disabled

The first scan attempt failed because the operation was canceled by the user.

The second scan completed successfully.

### Final Scan Result

- Status: Success
- Start: 9/10/2026 2:47 PM
- End: 9/10/2026 3:17 PM
- APP01 Scan: Success
- Malware Scan Test: Success

The `FLR_[app01]` session shown during the scan is an internal session created by the backup scanning process. It is not the File-Level Restore task.

## Result

Task 7 was completed successfully.

- Backup exists: Yes
- Restore Point available: Yes
- Malware Scan: Success
- Backup Job: Success
- Errors: 0
- Warnings: 0

## Status

<img width="1674" height="932" alt="image" src="https://github.com/user-attachments/assets/7100bcea-e5fc-4041-a768-810e7793b0b4" />

**Completed**
زظ
