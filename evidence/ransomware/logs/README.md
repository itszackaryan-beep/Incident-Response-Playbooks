# Logs Folder

This folder contains sample log outputs collected during the ransomware simulation performed in a controlled VMware Workstation lab environment.

## Environment

- Windows Server 2022
- Microsoft Sysmon
- Splunk Enterprise
- VMware Workstation

## Log Files

| File | Description |
|------|-------------|
| Sysmon_Process_Events.txt | Process Creation (Event ID 1) events generated during the simulation |
| File_Activity_Events.txt | File Create (Event ID 11) and file activity events collected by Sysmon |
| Ransom_Note_Events.txt | Events related to the simulated ransom note (README_RESTORE_FILES.txt) |

> These logs were generated in a safe educational lab environment. No real ransomware was executed and no files were encrypted.
