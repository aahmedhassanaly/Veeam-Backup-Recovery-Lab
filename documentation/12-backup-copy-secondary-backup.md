# Task 12 — Backup Copy / Secondary Backup

## Objective

Create a secondary copy of the `app01` backup using a Veeam Backup Copy Job.

The goal is to maintain another copy of the backup in a separate backup repository for additional data protection and recovery options.

---

## Environment

- Veeam Backup & Replication: 13.1.1.18
- Source Server: `app01`
- Primary Repository: `VEEAM01-Repository`
- Backup Copy Job: `app01-BackupCopy`

---

## Configuration

A new **Backup Copy Job** was created from:

**Home → Backup Copy → Backup Copy Job**

### Copy Mode

Selected:

**Immediate copy (mirroring)**

This mode copies new restore points to the target repository as soon as they become available in the primary backup repository.

### Objects

The existing `app01` backup job was selected as the source object.

### Target

The target repository was configured as:

`VEEAM01-Repository`

Retention policy:

`7 days`

---

## Verification

The Backup Copy Job was started manually.

The job completed successfully.

Results:

- Jobs: **1**
- Objects: **1**
- Processed: **1**
- Status: **Success**
- Warnings: **0**
- Errors: **0**
- Data processed: **19.9 GB**
- Data read: **19.9 GB**
- Data transferred: **11.8 GB**
- Duration: **2 minutes 8 seconds**

The session confirmed:

**Backup copy for app01 - 10.10.20.8 — Success**

---

## Result
 <img width="1236" height="850" alt="image" src="https://github.com/user-attachments/assets/6abe12ba-ed86-42a1-9ff9-bd3a85e88a48" />

**Task 12 completed successfully.**

A secondary backup copy of `app01` was created using Veeam Backup Copy Job.

### Backup Flow

```text
app01
   |
   v
Primary Backup
   |
   v
VEEAM01-Repository
   |
   v
Backup Copy Job
   |
   v
Secondary Backup Copy
