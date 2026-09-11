# Backup Failure Troubleshooting

## Objective

Troubleshoot a failed Veeam backup caused by loss of network connectivity between the Veeam Backup Server and the protected computer.

## Environment

- Veeam Backup Server: VEEAM01
- Protected Computer: APP01
- APP01 IP: 10.10.20.4
- Backup Job: APP01-Backup

## Task

A controlled failure was created by disabling the Ethernet adapter on APP01.

The network adapter was disabled with:

    Disable-NetAdapter -Name "Ethernet" -Confirm:$false


## Backup Failure

The `APP01-Backup` job was started from VEEAM01.

The job failed with:

    A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.

## Troubleshooting

### Problem

VEEAM01 could not communicate with APP01.




### Root Cause

The Windows network adapter on APP01 had been disabled.

The backup failed because VEEAM01 could not reach the protected computer.


## Troubleshooting Method

The incident followed:

    Problem → Evidence → Hypothesis → Test → Fix → Verify

The main lesson is to verify connectivity and the protected machine before changing Veeam configuration.

## Result

- Backup failure was successfully reproduced.
- The Veeam error was identified.
- The network connectivity problem was identified as the cause.
- APP01 and its Google Cloud network interface were verified.
- Recovery methods were investigated.
- No destructive recovery operation was performed.

## Status
 <img width="1665" height="915" alt="image" src="https://github.com/user-attachments/assets/fb86bb47-9bb7-46c1-8ca8-92d27087fba6" />

**Completed — Backup Failure Troubleshooting**

