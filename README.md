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

## Main Workflow

| Task | Area | Result |
|---|---|---|
| 01–05 | Cloud, Veeam, workload, infrastructure, repository | ✅ |
| 06–07 | Backup and verification | ✅ |
| 08–09 | File-level, volume, and bare-metal recovery | ✅ |
| 10 | Backup failure troubleshooting | ✅ |
| 11 | Application-Aware Processing / VSS | ✅ |
| 12 | Backup Copy | ✅ |
| 13 | Full-machine recovery to GCE | ✅ |

Detailed implementation notes are available in [Documentation](documentation/).

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
