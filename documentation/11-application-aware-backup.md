# Task 11 — Application-Aware Backup (VSS)

## Objective

Configure Application-Aware Processing for the Windows Server `app01` backup job.

The goal is to use Windows VSS (Volume Shadow Copy Service) during backup so that supported applications can be processed in a consistent state.

---

## Environment

- Veeam Backup & Replication: 13.1.1.18
- Protected Server: `app01`
- Operating System: Windows Server 2022
- Backup Job: `app01`
- Backup Agent: Veeam Agent for Microsoft Windows

---

## Configuration

The `app01` backup job was edited from:

**Home → Jobs → Backup → app01 → Edit**

Under **Guest Processing**:

- Enabled **Application-Aware Processing**
- VSS processing was configured as **Require successful processing**
- No custom scripts were configured

The configuration was saved and the backup job was started manually.

---

## Backup Verification

The backup job completed successfully.

Results:

- Status: **Success**
- Hosts processed: **1 of 1**
- Warnings: **0**
- Errors: **0**
- Total size: **50 GB**
- Data read: **1.3 GB**
- Transferred: **101.4 MB**
- Backup size: **110.6 MB**
- Duration: **2 minutes 45 seconds**

The Veeam session confirmed:

**Agent Backup job: app01 — Success — 1 of 1 hosts processed**

---

## VSS Verification

Application-Aware Processing was successfully configured and the backup completed without errors.

However, the available Veeam session report did not show detailed VSS processing information. Therefore, detailed VSS execution was not independently verified from the session report.

No SQL Server is installed on `app01`, so SQL-specific application consistency was not tested.

---

## Result
<img width="1284" height="836" alt="image" src="https://github.com/user-attachments/assets/826394a4-63d7-44ae-8097-f3d0f435014a" />

**Task 11 completed.**

