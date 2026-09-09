# Task 5 — Backup Repository

## Objective

Create a Veeam Backup Repository to store backup files.

For this lab, the repository is located on VEEAM01 to keep the environment simple and reduce cost.

## Lab Architecture

    APP01
       |
       | Backup
       v
    VEEAM01
       |
       v
    D:\VeeamRepository

## Repository Details

- Repository Name: VEEAM01-Repository
- Repository Server: VEEAM01
- Repository Path: D:\VeeamRepository
- File System: NTFS
- Capacity: about 100 GB
- Free Space: about 99.9 GB

## Step 1 — Add a Dedicated Disk

A second Persistent Disk was added to VEEAM01 in Google Cloud.

The disk was checked from PowerShell:

    Get-Disk

The server had:

- Disk 0 — 100 GB — Windows OS disk
- Disk 1 — 100 GB — backup storage disk

## Step 2 — Verify the Partition

The partition on Disk 1 was checked:

    Get-Partition -DiskNumber 1

Disk 1 had a basic partition using drive letter D:.

## Step 3 — Verify the File System

The D: drive was checked:

    Get-Volume -DriveLetter D

The result showed:

- File System: NTFS
- Health Status: Healthy
- Operational Status: OK
- Size: about 100 GB

## Step 4 — Create the Repository Folder

The folder for the backup files was created:

    New-Item -Path "D:\VeeamRepository" -ItemType Directory

The final path is:

    D:\VeeamRepository

## Step 5 — Create the Veeam Repository

In Veeam Backup & Replication:

    Backup Infrastructure
    → Backup Repositories
    → Add Repository

The repository was configured as:

- Type: Direct attached storage → Microsoft Windows
- Name: VEEAM01-Repository
- Server: VEEAM01
- Path: D:\VeeamRepository

## Fast Clone Warning

Veeam displayed a warning because the repository uses NTFS and does not support Fast Clone.

Fast Clone is available with suitable ReFS storage.

For this lab, the warning was accepted and the NTFS repository was used.

We did not reformat the disk because Fast Clone is not required for this lab.

## Mount Server

The Windows Mount Server was configured as:

    VEEAM01 (Backup server)

The Linux Mount Server was left as:

    Not specified

The Mount Server can be used during restore operations such as file-level and other advanced restore operations.

## Existing Backup Import

The option to search for existing backups was left disabled because this is a new and empty repository.

## Verification

The repository was successfully created and appeared under:

    Backup Infrastructure
    → Backup Repositories

The final repository showed:

- Name: VEEAM01-Repository
- Type: Windows
- Host: VEEAM01
- Path: D:\VeeamRepository
- Capacity: about 100 GB
- Free Space: about 99.9 GB

## Important Concept

The Veeam Backup Server manages backup operations.

The Backup Repository is the location where Veeam stores the backup files.

Example:

    APP01
       |
       | Backup
       v
    VEEAM01
       |
       v
    D:\VeeamRepository
       |
       +-- Backup Files

## Production Note

Using the same server as the Veeam Backup Server and Backup Repository is acceptable for this lab.

In production, the repository is normally separated from the Veeam management server for better security, isolation, and resilience.

## What I Learned

- A Backup Repository stores Veeam backup files.
- A dedicated disk can be used for backup storage.
- A Windows folder can be used as a repository path.
- NTFS works for the lab but does not provide Fast Clone.
- A Mount Server is used during restore operations.
- The Backup Server and Repository can be combined in a small lab.

## Status

Task 5 — Backup Repository: COMPLETE
<img width="1692" height="836" alt="image" src="https://github.com/user-attachments/assets/48be0f06-461e-4431-a9a3-e95bedb311d1" />

