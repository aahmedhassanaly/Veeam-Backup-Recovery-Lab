# Veeam Backup & Recovery Lab

A practical Veeam Backup & Replication lab built on Google Cloud to simulate backup, recovery, troubleshooting, application-aware processing, backup copy, and disaster recovery workflows.

The lab focuses on hands-on infrastructure skills rather than only following product tutorials.

## Lab Objectives

- Deploy a Veeam Backup & Replication environment.
- Protect a Windows Server workload with Veeam Agent for Microsoft Windows.
- Create and manage backup repositories and backup jobs.
- Verify backup sessions and recovery points.
- Perform file-level, volume, and full-machine recovery operations.
- Troubleshoot a failed backup using evidence-based investigation.
- Configure Application-Aware Processing with Windows VSS.
- Create a secondary backup copy with a Backup Copy Job.
- Perform a full-machine disaster recovery test to Google Compute Engine.
- Verify the recovered VM through networking and RDP access.

## Architecture

### Topology

> **Topology image will be added here.**
>
> Recommended file: `images/veeam-lab-topology.png`

![Veeam Lab Topology](images/veeam-lab-topology.png)

## Environment

| Component | Details |
|---|---|
| Cloud Platform | Google Cloud Platform |
| Region | `me-central1` |
| Zone | `me-central1-a` |
| VPC | `veeam-vpc` |
| Subnet | `veeam-subnet-me` |
| Veeam Server | `VEEAM01` |
| Veeam Server OS | Windows Server 2022 |
| Protected Workload | `APP01` |
| Workload OS | Windows Server 2022 |
| Recovery VM | `app01new` |
| Veeam Version | 13.1.1.18 |
| Target Recovery Platform | Google Compute Engine |

## Main Components

### VEEAM01

The Veeam management and backup server running Veeam Backup & Replication.

### APP01

The protected Windows Server 2022 workload used for backup and recovery testing.

### VEEAM01-Repository

The backup repository used to store the primary backup data and backup copy data in this lab.

### app01new

A new Google Compute Engine VM created during the disaster recovery test from the `APP01` backup.

## Lab Workflow

The lab was completed progressively from infrastructure setup to recovery validation.

### 1. Google Cloud Environment Setup

Created the required Google Cloud networking and compute environment for the Veeam lab.

### 2. Veeam Installation

Installed and prepared Veeam Backup & Replication on `VEEAM01`.

### 3. Protected Workload

Prepared `APP01` as the Windows Server 2022 workload to be protected.

### 4. Veeam Infrastructure Setup

Configured the Veeam infrastructure and connected the required components.

### 5. Backup Repository

Created and configured `VEEAM01-Repository` for backup storage.

### 6. First Backup Job

Created the primary backup job for `APP01` and executed a successful backup.

### 7. Analyze, Verify, and Manage Backup

Reviewed backup sessions, restore points, data processing information, and job results.

### 8. File-Level Restore

Performed file-level recovery from the backup to verify granular recovery capability.

### 9. Volume and Bare-Metal Recovery

Practiced volume-level and bare-metal recovery workflows available from the lab backup set.

### 10. Backup Failure Troubleshooting

Investigated a failed backup scenario using a practical troubleshooting approach based on evidence, hypothesis, testing, fixing, and verification.

### 11. Application-Aware Backup (VSS)

Enabled Application-Aware Processing for `APP01` and configured VSS processing as **Require successful processing**.

The backup completed successfully with:

- Status: `Success`
- Hosts processed: `1 of 1`
- Warnings: `0`
- Errors: `0`
- Total size: `50 GB`
- Data read: `1.3 GB`
- Transferred: `101.4 MB`
- Backup size: `110.6 MB`
- Duration: `2 minutes 45 seconds`

Detailed VSS execution information was not independently visible in the available session report, so the lab does not claim detailed VSS validation. SQL-specific consistency was also not tested because SQL Server was not installed on `APP01`. fileciteturn7file0

### 12. Backup Copy / Secondary Backup

Created a Veeam Backup Copy Job named `app01-BackupCopy` using **Immediate Copy (mirroring)**.

The copy used `VEEAM01-Repository` as the target repository with a retention policy of `7 days`.

Verification results:

- Status: `Success`
- Objects: `1`
- Warnings: `0`
- Errors: `0`
- Data processed: `19.9 GB`
- Data transferred: `11.8 GB`
- Duration: `2 minutes 8 seconds`

This demonstrates a second backup copy workflow, but the primary and secondary copies are still within the same lab infrastructure and should not be considered a fully independent off-site backup design. fileciteturn5file0

### 13. Disaster Recovery / Full Recovery to GCE

Performed a full-machine restore of `APP01` to Google Compute Engine as a new VM named `app01new`.

Recovery target:

- Project: `Veeam Infrastructure Lab`
- Region: `me-central1`
- Zone: `me-central1-a`
- VPC: `veeam-vpc`
- Subnet: `veeam-subnet-me`

Recovery results:

- Disk: `50 GB`
- Restored data: `19.9 GB`
- Disk conversion: `Success`
- Restore process: `Completed`
- Recovered VM: `app01new`
- Status: `RUNNING`
- Internal IP: `10.10.20.10`
- External IP: `34.18.136.139`

During validation, RDP initially failed because the recovered VM did not have the required `app01` network tag. After adding the tag required by the existing TCP/3389 firewall rule, RDP access was successfully established.

The original `APP01` VM was not modified during the recovery test. fileciteturn6file0

## Troubleshooting Approach

The lab used a structured troubleshooting method:

**Problem → Evidence → Hypothesis → Test → Fix → Verify**

Examples encountered during the lab included:

- Backup and guest-processing troubleshooting.
- Google Cloud organization policy restrictions affecting external IP access.
- Service account creation restrictions.
- VM Migration API and service-agent requirements.
- Recovery target configuration problems.
- RDP connectivity caused by a missing firewall target tag.

The goal was not only to make the task work, but to identify the actual cause and verify the fix.

## Recovery Flow

```text
APP01
  |
  v
Veeam Backup Job
  |
  v
VEEAM01-Repository
  |
  +----------------------+
  |                      |
  v                      v
Backup Copy          Full Machine Restore
                         |
                         v
                Google Compute Engine
                         |
                         v
                     app01new
                         |
                         v
                        RDP
```

## Skills Demonstrated

### Backup Administration

- Backup job creation and management
- Backup repository configuration
- Backup session analysis
- Restore point management
- Backup copy operations

### Recovery

- File-level restore
- Volume-level recovery
- Bare-metal recovery workflow
- Full-machine restore
- Cloud-based disaster recovery

### Windows Infrastructure

- Windows Server 2022
- Veeam Agent for Microsoft Windows
- VSS / Application-Aware Processing
- RDP troubleshooting

### Google Cloud

- Compute Engine
- VPC networking
- Firewall rules and network tags
- IAM and service accounts
- Required API enablement
- VM recovery into GCE
- Cloud troubleshooting during recovery

### Troubleshooting

- Reading job/session results
- Identifying infrastructure restrictions
- Testing hypotheses before applying fixes
- Verifying recovered systems after changes

## Documentation

Detailed implementation notes are available in the `documentation/` directory.

| Task | Documentation |
|---|---|
| 01 | `documentation/01-google-cloud-environment-setup.md` |
| 02 | `documentation/02-veeam-installation.md` |
| 03 | `documentation/03-app01-workload.md` |
| 04 | `documentation/04-veeam-infrastructure-setup.md` |
| 05 | `documentation/05-backup-repository.md` |
| 06 | `documentation/06-first-backup-job.md` |
| 07 | `documentation/07-analyze-verify-manage-backup.md` |
| 08 | `documentation/08-file-level-restore.md` |
| 09 | `documentation/09-volume-bare-metal-recovery.md` |
| 10 | `documentation/10-backup-failure-troubleshooting.md` |
| 11 | `documentation/11-application-aware-backup.md` |
| 12 | `documentation/12-backup-copy-secondary-backup.md` |
| 13 | `documentation/13-disaster-recovery-full-recovery-to-gce.md` |

## Important Lab Limitations

This is a practical learning lab, not a complete production backup and disaster recovery architecture.

- The primary and backup-copy data use the same lab infrastructure.
- The environment does not provide a fully independent off-site backup site.
- Detailed VSS application consistency was not independently verified from the Veeam session report.
- SQL Server application consistency was not tested.
- The GCE recovery demonstrates technical recovery capability, but not a complete enterprise DR strategy.

## Final Result

The lab demonstrates an end-to-end Veeam backup and recovery workflow:

**Windows Workload → Veeam Backup → Repository → Backup Copy → Recovery → Google Cloud DR**

The project was intentionally stopped after the full recovery objective was completed because additional Veeam tasks in the same environment would add limited learning value compared with building a separate virtualization-focused lab.
