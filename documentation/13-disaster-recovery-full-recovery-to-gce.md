# 13 - Disaster Recovery / Full Recovery to GCE

## Objective

Restore the `APP01` server from a Veeam backup to Google Compute Engine as a new virtual machine.

The original `APP01` VM must remain unchanged.

## Environment

- Veeam Server: `VEEAM01`
- Backup Repository: `VEEAM01-Repository`
- Source VM: `APP01`
- Target Platform: Google Compute Engine
- GCP Project: `Veeam Infrastructure Lab`
- Region: `me-central1`
- Zone: `me-central1-a`
- VPC: `veeam-vpc`
- Subnet: `veeam-subnet-me`
- Recovery VM: `app01new`

## Recovery Steps

### 1. Start the Restore

In Veeam:

`Home → Restore → Entire machine restore → Restore to public cloud → Google Compute Engine`

Select the required `APP01` backup.

### 2. Configure the GCE Target

Configure the recovery target:

- Project: `Veeam Infrastructure Lab`
- Region: `me-central1`
- Zone: `me-central1-a`
- VPC: `veeam-vpc`
- Subnet: `veeam-subnet-me`

Restore the machine as a new VM:

`app01new`

### 3. Complete the Restore

Veeam successfully restored the backup disk and converted it for Google Compute Engine.

- Restoring Disk 0: `50 GB`
- Restored data: `19.9 GB`
- Converting disks (GCE): `Success`
- Restore process: `Completed`
<img width="1117" height="756" alt="image" src="https://github.com/user-attachments/assets/44b02c4b-66d9-4518-9d93-b3ef12650c3e" />

## Verification

The recovered VM was successfully created in Google Cloud.

- VM Name: `app01new`
- Zone: `me-central1-a`
- Status: `RUNNING`
- Internal IP: `10.10.20.10`
- External IP: `34.18.136.139`

Windows credentials were generated using:

`gcloud compute reset-windows-password app01new --zone=me-central1-a --project=project-e754cd31-af6b-470d-a52`

## RDP Verification

RDP initially failed because the recovered VM did not have the network tag required by the RDP firewall rule.

The firewall rule required:

- Target tag: `app01`
- Protocol: `TCP`
- Port: `3389`

The required tag was added:

`gcloud compute instances add-tags app01new --zone=me-central1-a --project=project-e754cd31-af6b-470d-a52 --tags=app01`

The tag was verified successfully:

`app01`

RDP access was then successfully established.

## Result

The Disaster Recovery test was successful.

The `APP01` backup was restored as a new Google Compute Engine VM:

`Veeam Backup → VEEAM01-Repository → Full Machine Restore → Google Compute Engine → app01new → RDP`

The original `APP01` VM was not modified.
<img width="1880" height="972" alt="image" src="https://github.com/user-attachments/assets/b9981c35-6909-4225-8eb3-8c07c6d9839e" />

## Notes

This lab proves that the Veeam backup can be restored successfully to Google Compute Engine.

It does not represent a complete production DR design because the lab does not yet provide a fully independent off-site recovery infrastructure.
