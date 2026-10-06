# Veeam Backup & Recovery Lab

**Portfolio Priority: #4 — Backup, Recovery & Disaster Recovery**

A practical **Veeam Backup & Replication** lab built on Google Cloud. The project covers backup administration, recovery, application-aware processing, backup copy, disaster recovery, and troubleshooting.

## Objectives

- Deploy Veeam Backup & Replication
- Protect a Windows Server workload
- Configure repositories and backup jobs
- Verify backup sessions and recovery points
- Perform file-level, volume, and full-machine recovery
- Troubleshoot backup failures using evidence
- Configure Application-Aware Processing with Windows VSS
- Create a secondary backup copy
- Recover a full machine to Google Compute Engine
- Validate the recovered VM through networking and RDP

## Architecture

<img width="1536" height="1024" alt="Veeam backup and recovery topology" src="https://github.com/user-attachments/assets/039f77f3-2dd6-431b-1b4c-46100d687267" />

```text
APP01
  |
  v
Veeam Backup
  |
  v
Repository
  |
  +------ Backup Copy
  |
  +------ Full Machine Restore
                 |
                 v
          Google Compute Engine
                 |
                 v
              app01new
```

## Environment

| Component | Details |
|---|---|
| Cloud Platform | Google Cloud Platform |
| Region / Zone | `me-central1 / me-central1-a` |
| VPC | `veeam-vpc` |
| Subnet | `veeam-subnet-me` |
| Veeam Server | `VEEAM01` |
| Veeam OS | Windows Server 2022 |
| Protected Workload | `APP01` |
| Recovery VM | `app01new` |
| Veeam Version | 13.1.1.18 |
| Recovery Target | Google Compute Engine |

## Tasks

| # | Task | Status |
|---:|---|:---:|
| 01 | [Google Cloud Environment Setup](documentation/01-google-cloud-environment-setup.md) | ✅ |
| 02 | [Veeam Backup & Replication Installation](documentation/02-veeam-installation.md) | ✅ |
| 03 | [Prepare APP01 Workload](documentation/03-app01-workload.md) | ✅ |
| 04 | [Veeam Infrastructure Setup](documentation/04-veeam-infrastructure-setup.md) | ✅ |
| 05 | [Backup Repository](documentation/05-backup-repository.md) | ✅ |
| 06 | [First Backup Job](documentation/06-first-backup-job.md) | ✅ |
| 07 | [Analyze, Verify & Manage Backup](documentation/07-analyze-verify-manage-backup.md) | ✅ |
| 08 | [File-Level Restore](documentation/08-file-level-restore.md) | ✅ |
| 09 | [Volume & Bare-Metal Recovery](documentation/09-volume-bare-metal-recovery.md) | ✅ |
| 10 | [Backup Failure Troubleshooting](documentation/10-backup-failure-troubleshooting.md) | ✅ |
| 11 | [Application-Aware Backup](documentation/11-application-aware-backup.md) | ✅ |
| 12 | [Backup Copy & Secondary Backup](documentation/12-backup-copy-secondary-backup.md) | ✅ |
| 13 | [Disaster Recovery — Full Recovery to GCE](documentation/13-disaster-recovery-full-recovery-to-gce.md) | ✅ |

Detailed implementation notes: [Documentation](documentation/).

## Key Evidence

- Successful backup session
- Application-Aware Processing configured as **Require successful processing**
- Successful Backup Copy job
- Full-machine restore completed
- Recovered VM reached `RUNNING`
- RDP recovery issue identified and fixed by correcting the required GCE network tag

The VSS session report did not independently expose detailed VSS execution evidence, so the project does not claim detailed VSS validation. SQL-specific consistency was not tested because SQL Server was not installed.

## Troubleshooting Method

**Problem → Evidence → Hypothesis → Test → Fix → Verify**

Examples include backup failures, guest-processing issues, Google Cloud policy restrictions, recovery-target requirements, and RDP connectivity.

## Lab Limitations

- Primary and backup-copy data use the same lab infrastructure.
- No fully independent off-site backup site was implemented.
- SQL application consistency was not tested.
- GCE recovery demonstrates technical recovery capability, not a complete enterprise DR strategy.

## Result

**Windows Workload → Veeam Backup → Repository → Backup Copy → Recovery → Google Cloud DR**

The lab was stopped after Task 13 because the main recovery objective was complete; additional Veeam tasks in the same environment would add less value than a separate virtualization-focused lab.
