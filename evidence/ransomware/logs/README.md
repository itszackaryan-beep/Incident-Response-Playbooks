# Logs

## Overview

This directory contains the log files, exported event data, and Splunk search queries collected during the ransomware detection lab.

The logs were generated from a safe ransomware simulation performed on **Windows Server 2022** using **Microsoft Sysmon** and analyzed in **Splunk Enterprise**.

No real ransomware was executed during this project. All activities were performed in a controlled lab environment for educational purposes.

---

# Contents

## EventID_1_Process_Create.xml

Contains Microsoft Sysmon **Process Creation (Event ID 1)** logs generated during the simulation.

The events include process execution such as:

- cmd.exe
- powershell.exe
- notepad.exe

These logs help identify suspicious process execution during incident investigations.

---

## EventID_11_File_Create.xml

Contains Microsoft Sysmon **File Create (Event ID 11)** logs.

The recorded events include:

- Test folder creation
- File creation
- Simulated ransom note creation
- README_RESTORE_FILES.txt

These logs demonstrate how ransomware-related file activity can be detected.

---

## IOC_Extraction.csv

Contains extracted Indicators of Compromise (IOCs) from Splunk.

The exported data includes:

- Timestamp
- Host Name
- User
- Process Name
- File Name
- Event ID
- Target Filename

This information is useful during forensic investigations and incident response.

---

## Splunk_Search_Query.txt

Contains all Splunk SPL queries used throughout the project.

Example queries include:

- Process Creation Detection
- File Creation Detection
- IOC Extraction
- Ransom Note Detection

These queries can be reused to reproduce the investigation.

---

# Detection Sources

- Microsoft Sysmon
- Windows Event Logs
- Splunk Enterprise

---

# Purpose

The purpose of these log files is to provide supporting evidence for the ransomware simulation and demonstrate how Microsoft Sysmon and Splunk Enterprise can be used to detect and investigate ransomware-like activity in a controlled cybersecurity lab.

---

# Note

This project is intended for educational purposes only.

No malicious software was executed, and no files were encrypted. All ransomware-related activities shown in this repository are safe simulations designed for cybersecurity learning and incident response practice.
