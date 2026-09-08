# Task 4 — Veeam Infrastructure Setup

## Objective

Prepare the basic Veeam infrastructure and connect the workload server to Veeam Backup & Replication.

The goal is to understand how Veeam communicates with a protected Windows workload and how the main Veeam components work together.

## Veeam Environment

The lab contains:

- `VEEAM01` — Veeam Backup & Replication server
- `APP01` — Windows workload that will be protected by Veeam

`VEEAM01` is the main management server.

`APP01` contains the test data that will be backed up later.

## Protection Group

Because `APP01` is a physical-style Windows workload from Veeam's perspective, it was added using a Veeam Protection Group.

The Protection Group was configured with:

- Computer: `10.10.20.4`
- Connection type: Windows computer
- Distribution server: `VEEAM01`
- Veeam Agent installation: Enabled
- Automatic agent update: Enabled
- Automatic reboot: Disabled

Veeam was configured to use administrative credentials to connect to `APP01` and deploy the Veeam Agent.

## Initial Deployment Problem

The first Protection Group rescan failed.

Veeam reported that it could not connect to the deployment components on `APP01` using ports:

- TCP `6160`
- TCP `11731`

Additional network testing from `VEEAM01` showed that TCP `445` was also unreachable.

This indicated a communication problem between `VEEAM01` and `APP01`.

## Troubleshooting

The problem was investigated using the following approach:

Problem → Evidence → Hypothesis → Test → Fix → Verify

### Problem

Veeam could not deploy the Veeam Agent to `APP01`.

### Evidence

Network tests from `VEEAM01` initially showed that communication with `APP01` was failing.

TCP `445`, `6160`, and `11731` were not reachable.

Ping was also unsuccessful.

### Investigation

The Windows Firewall on `APP01` was checked.

File and Printer Sharing inbound rules were disabled, so these rules were enabled to allow the required Windows management and SMB communication.

SMB was also verified:

- SMB2 was enabled.
- The Server service was running.
- Administrative shares such as `ADMIN$` were available.

However, communication was still not working correctly.

The Google Cloud internal firewall rule was then checked.

The lab subnet was:

`10.10.20.0/24`

The existing internal firewall rule was incorrectly configured with:

`10.10.0.0/24`

The configured source range did not include the actual lab subnet.

### Fix

The Google Cloud internal firewall rule was updated:

    gcloud compute firewall-rules update veeam-allow-internal \
      --source-ranges=10.10.20.0/24

This allowed internal communication between `VEEAM01` and `APP01`.

### Verification

Connectivity to the SMB service was tested again from `VEEAM01`:

    Test-NetConnection 10.10.20.4 -Port 445

The test succeeded.

Administrative share access was also verified:

    net use \\10.10.20.4\admin$ /user:APP01\ahmed *

The command completed successfully.

This confirmed that:

- Network connectivity was working.
- SMB communication was working.
- The `ADMIN$` administrative share was accessible.
- The supplied administrative credentials were valid.

The Protection Group was then rescanned from Veeam.

The rescan completed successfully and `APP01` appeared as `Online`.

## Result

`APP01` was successfully added to Veeam Backup & Replication through a Protection Group.

The Veeam Agent deployment process was successfully completed.

The lab now has:

- `VEEAM01` — Veeam Backup & Replication server
- `APP01` — protected Windows workload

<img width="1718" height="898" alt="image" src="https://github.com/user-attachments/assets/3d6be82d-1475-44d1-a3d3-f9cc7e2fe60d" />

