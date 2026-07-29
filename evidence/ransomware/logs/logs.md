# Logs

## Overview

This directory contains the log files, exported event data, and Splunk search queries collected during the ransomware detection and investigation lab.

The logs were generated from a **safe ransomware simulation** performed on **Windows Server 2022** using **Microsoft Sysmon** and analyzed in **Splunk Enterprise**.

No real ransomware was executed during this project. All activities were performed in a controlled VMware Workstation lab environment for educational and defensive cybersecurity purposes.

---

# Contents

## Sysmon_Process_Events.txt

Contains Microsoft Sysmon **Process Creation (Event ID 1)** logs generated during the simulation.

The recorded events include:

- cmd.exe
- powershell.exe
- notepad.exe
- whoami
- ipconfig
- tasklist

These logs demonstrate how Microsoft Sysmon records process execution for endpoint monitoring and incident investigations.

---

## File_Activity_Events.txt

Contains Microsoft Sysmon **File Create (Event ID 11)** logs generated during the ransomware simulation.

The recorded activities include:

- Test folder creation
- Test file creation
- File rename operations
- File modification
- File deletion
- Simulated ransomware file activity

These logs demonstrate how ransomware-like file behavior can be detected using Microsoft Sysmon and Splunk Enterprise.

---

## Ransom_Note_Events.txt

Contains log information related to the simulated ransom note created during the lab.

The recorded activity includes:

- README_RESTORE_FILES.txt creation
- File Create (Event ID 11)
- Ransom note detection in Splunk Enterprise

This demonstrates how defenders can detect one of the most common indicators of ransomware attacks.

---

## IOC_Extraction.txt

Contains Indicators of Compromise (IOCs) extracted from Splunk Enterprise.

The collected information includes:

- Timestamp
- Host Name
- User
- Process Name
- File Name
- Event ID
- Target Filename

These artifacts can be used during digital forensics and incident response investigations.

---

## Splunk Search Queries

The following Splunk SPL queries were used during the investigation:

### Process Creation Detection

```spl
index=main EventCode=1
```

### File Activity Detection

```spl
index=main EventCode=11
```

### IOC Extraction

```spl
index=main (EventCode=1 OR EventCode=11)
| table _time host Image TargetFilename User EventCode
```

### Ransom Note Detection

```spl
index=main EventCode=11
```

---

# Detection Sources

- Microsoft Sysmon
- Windows Event Logs
- Splunk Enterprise

---

# Purpose

The purpose of these log files is to provide supporting evidence for the ransomware detection project and demonstrate how Microsoft Sysmon and Splunk Enterprise can be used to detect, monitor, and investigate ransomware-like behavior in a controlled cybersecurity lab.

The project covers:

- Process Creation Monitoring
- File Activity Monitoring
- Simulated Ransom Note Detection
- IOC Extraction
- Incident Investigation

---

# Note

This repository is intended **for educational purposes only**.

No malicious software was executed.

No files were encrypted.

All ransomware-related activities shown in this repository are **safe simulations** designed for cybersecurity learning, SOC Analyst training, and incident response practice.
