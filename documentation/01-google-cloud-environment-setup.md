# Task 1 — Google Cloud Environment Setup

## Objective

Prepare the basic Google Cloud environment for the Veeam lab.

Google Cloud is used only to host the lab because the local hardware is not suitable for running Veeam.

## Network

The lab uses the following network configuration:

* VPC: `veeam-vpc`
* Subnet: `veeam-subnet-me`
* Region: `me-central1`
* Zone: `me-central1-a`
* Subnet CIDR: `10.10.20.0/24`
* Gateway: `10.10.20.1`

An internal firewall rule was configured for communication between lab resources.

## Storage

A Cloud Storage bucket was created for the Veeam lab:

* Bucket: `veeam-backup-project-e754cd31-af6b-470d-a52`
* Location: `me-central1`
* Storage class: `STANDARD`

This bucket will be used later as part of the backup environment.

## Service Account

A service account was created for Veeam:

`veeam-gcp@project-e754cd31-af6b-470d-a52.iam.gserviceaccount.com`

A custom IAM role was assigned instead of giving the account full Owner permissions.

## VEEAM01

A Windows Server 2022 VM was created to run Veeam Backup & Replication.

* Hostname: `veeam01`
* Machine type: `e2-standard-8`
* CPU: 8 vCPU
* RAM: 32 GB
* Boot disk: 100 GB
* Disk type: `pd-balanced`
* Internal IP: `10.10.20.3`
* Network: `veeam-vpc`
* Subnet: `veeam-subnet-me`

RDP access was configured so the server can be managed remotely.

## Verification

The server was accessed successfully through RDP.

Network configuration was checked:

* IP: `10.10.20.3`
* Subnet mask: `255.255.255.0`
* Gateway: `10.10.20.1`

Internet connectivity was tested successfully using HTTPS.

## Result

The basic Google Cloud environment is ready.

`VEEAM01` is running, accessible through RDP, and has working network connectivity.

The next task is to prepare the workload VM that will be protected by Veeam.
