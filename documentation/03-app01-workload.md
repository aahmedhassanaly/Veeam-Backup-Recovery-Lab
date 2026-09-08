# Task 3 — Prepare APP01 Workload

## Objective

Prepare a Windows Server VM that will act as the workload protected by Veeam.

`APP01` is the machine that contains the test data, while `VEEAM01` runs Veeam Backup & Replication.

## APP01

The VM was created in Google Cloud with the following configuration:

- Hostname: `app01`
- OS: Windows Server 2022
- Machine type: `e2-standard-2`
- CPU: 2 vCPU
- RAM: 8 GB
- Boot disk: 50 GB
- Disk type: `pd-balanced`
- Zone: `me-central1-a`
- Network: `veeam-vpc`
- Subnet: `veeam-subnet-me`
- Internal IP: `10.10.20.4`
- Public IP: Enabled

## Remote Access

RDP access was configured for `APP01`.

A firewall rule was created to allow TCP port `3389` for the `app01` network tag.

The server was successfully accessed through Remote Desktop.

## Test Data

A small test dataset was created on `APP01` to verify future backup and restore operations.

Folder:

`C:\LabData`

Test file:

`C:\LabData\important-data.txt`

The file contains:

`Veeam Backup Lab - Original Data`

This data will be used later to verify that backup and restore operations actually recover the expected data.

## Verification

The following was verified:

- `APP01` is running.
- RDP access is working.
- The workload VM is reachable.
- Test data was created successfully.

## Result

`APP01` is ready as the workload for the Veeam lab.
<img width="1798" height="1006" alt="image" src="https://github.com/user-attachments/assets/4d74e508-53e2-4f43-b99f-8de5a99155e1" />

The next task is to deploy the Veeam Backup Appliance and prepare the Google Cloud integration.
