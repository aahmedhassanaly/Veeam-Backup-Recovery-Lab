# Task 6 — First Backup Job

## Objective

Create and run the first Veeam Agent Backup Job for APP01.

The goal is to create an image-based backup of the entire APP01 computer and store the backup files in the VEEAM01 backup repository.

---

## Environment

- Backup Server: VEEAM01
- Workload: APP01
- Operating System: Windows Server 2022
- Backup Type: Windows Agent Backup
- Backup Mode: Entire computer
- Backup Repository: VEEAM01-Repository
- Repository Path: D:\VeeamRepository
- Repository Size: 100 GB

---

## 1. Create the Backup Job

From the Veeam Backup & Replication Console:

Home → Backup Job → Windows computer

### Job Mode

- Type: Server
- Mode: Managed by backup server

### Computers

Select:

- APP01

The APP01 computer was already added to Veeam through the Protection Group.

---

## 2. Backup Mode

Select:

- Entire computer

This creates an image-based backup of the whole computer.

The backup can be used for full computer recovery and other restore operations.

Temporary files and page files are automatically excluded from the image.

---

## 3. Storage

Select:

- Backup Repository: VEEAM01-Repository
- Repository path: D:\VeeamRepository
- Retention: 7 days

The backup files are stored on the separate 100 GB disk attached to VEEAM01.

The data flow is:

APP01 → Veeam Agent → VEEAM01 → D:\VeeamRepository

---

## 4. Guest Processing

Application-aware processing was enabled.

Guest file system indexing and malware detection were not enabled for this lab.

Application-aware processing helps Veeam create a more consistent backup for applications that support it.

---

## 5. Schedule

Automatic scheduling was not enabled for the initial test.

The first backup was started manually to verify that the complete backup workflow works correctly.

---

## 6. Run the Backup

The job was started manually from:

Home → Jobs → Backup

Job:

APP01-Backup

---

## 7. Backup Result

The first backup completed successfully.

Results:

- Job: APP01-Backup
- Workload: APP01
- Result: Success
- Errors: 0
- Warnings: 0
- Duration: 8 minutes 56 seconds
- Processed: 22 GB
- Read: 20.6 GB
- Transferred: 12.3 GB
- Processing rate: 153 MB/s
- Primary bottleneck: Source

The job successfully processed APP01 and created the first backup restore point.

---

## What I Learned

A Veeam Agent Backup can protect a Windows computer by creating an image-based backup.

The backup data is not stored on APP01. It is sent to the configured Backup Repository.

In this lab:

APP01
→ Veeam Agent
→ VEEAM01
→ VEEAM01-Repository
→ D:\VeeamRepository

The difference between Processed, Read, and Transferred is important:

- Processed: Total amount of data that Veeam processed.
- Read: Amount of data read from the source.
- Transferred: Amount of data actually sent to the repository after Veeam processing.

The first backup confirmed that the complete backup path is working.

---

## Verification

The backup job finished with:

- Success: 1
- Warnings: 0
- Errors: 0

Therefore, Task 6 is complete.

## Status

**Task 6 — COMPLETE**

<img width="1916" height="1031" alt="image" src="https://github.com/user-attachments/assets/a8d3ad12-eb22-451e-9fec-b7bc963cea46" />

