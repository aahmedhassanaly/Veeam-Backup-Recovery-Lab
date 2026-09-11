# Task 9 — Volume & Bare-Metal Recovery

## Objective

Understand and prepare for Volume Restore and Bare-Metal Recovery using Veeam Agent backups.

## Volume Restore

The `APP01-Backup` restore points were inspected from:

    Home → Backups → Disk → APP01-Backup

Two restore points were available.

The latest restore point was selected.

The backup contained:

- EFI system partition
- `C:` system volume

Veeam warned that the `C:` system volume cannot be restored over itself while Windows is running.

This is expected because the operating system is currently using the system volume.

## Recovery Media

A Veeam Recovery Media ISO was successfully created.

The Recovery Media contains the Veeam Recovery Environment and recovery tools.

It does not contain the complete Windows installation, applications, and user files from APP01.

The actual computer data is stored in the Veeam backup repository.

The recovery process is:

    Boot from Veeam Recovery Media
    ↓
    Start Veeam Recovery Environment
    ↓
    Connect to the Backup Repository
    ↓
    Select APP01 Backup
    ↓
    Select Restore Point
    ↓
    Restore Entire Computer
    ↓
    Reboot
    ↓
    Windows and protected data are recovered

## Bare-Metal Recovery

Bare-Metal Recovery is used when the operating system or system disk is no longer usable.

It can restore the complete computer, including:

- System partitions
- Windows operating system
- Applications included in the backup
- User data included in the backup

The Recovery Media is the tool used to boot the failed computer.

The Backup is the source containing the data that will be restored.

Therefore:

**Recovery ISO = Recovery Environment**

**Backup = Protected Computer Data**

## Lab Limitation

A complete Bare-Metal Restore was not executed in this lab because APP01 is hosted as a Google Cloud VM and the current environment does not provide the required boot-media workflow for safely booting APP01 from the Veeam Recovery ISO.

The Recovery Media was successfully created and the complete BMR workflow was understood, but the actual system-volume recovery was not performed.

No destructive restore was attempted on the running APP01 system.

## Result

- Volume Restore workflow reviewed: Yes
- System Volume restriction understood: Yes
- Recovery Media ISO created: Success
- Bare-Metal Recovery workflow understood: Yes
- Full Bare-Metal Restore executed: No
- APP01 remained operational: Yes

## Status
<img width="1035" height="780" alt="image" src="https://github.com/user-attachments/assets/70251b5a-6a3e-412e-b098-c0b967ed798c" />

**Completed — Recovery Preparation & BMR Workflow**

