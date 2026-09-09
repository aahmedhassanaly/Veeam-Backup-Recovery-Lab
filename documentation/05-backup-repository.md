# Task 5 — Backup Repository

## Objective

Create and configure a Veeam Backup Repository where backup files will be stored.

In this lab, the repository is hosted on the VEEAM01 server to keep the environment simple and reduce cost.

---

## Lab Architecture

<img width="1692" height="836" alt="image" src="https://github.com/user-attachments/assets/0de8263f-bd80-4562-827f-c265a6f1e281" />

```text
APP01
  |
  | Backup Data
  v
VEEAM01
  |
  +-- D:\VeeamRepository
          |
          +-- Veeam Backup Files

