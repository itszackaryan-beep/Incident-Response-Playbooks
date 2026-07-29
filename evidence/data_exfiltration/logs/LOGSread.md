# Logs

## Overview

This directory contains the log files, exported event data, and Splunk search queries collected during the **Data Exfiltration Detection and Investigation** lab.

The logs were generated from a safe data staging and archive creation simulation performed on **Windows Server 2022** using **Microsoft Sysmon** and analyzed in **Splunk Enterprise**.

No actual data exfiltration or unauthorized data transfer was performed during this project. All activities were conducted in a controlled cybersecurity lab environment for educational and defensive security purposes.

---

# Contents

## EventID_1_Process_Create.txt

Contains Microsoft Sysmon **Process Creation (Event ID 1)** logs generated during the simulation.

The recorded events include processes responsible for:

- File Explorer (explorer.exe)
- ZIP archive creation
- File management operations

These logs help investigators determine which process initiated the observed file activities.

---

## EventID_11_File_Create.txt

Contains Microsoft Sysmon **File Create (Event ID 11)** logs.

The recorded events include:

- Company_Data folder creation
- Dummy confidential file creation
- Collected_Data folder creation
- ZIP archive creation (Collected_Data.zip)

These logs demonstrate how Microsoft Sysmon records file activity that may indicate data staging before exfiltration.

---

## IOC_Extraction.txt

Contains the extracted **Indicators of Compromise (IOCs)** identified during the investigation.

The exported information includes:

- Timestamp
- Host Name
- User Account
- Process Name
- Target File Name
- Event ID

These artifacts support forensic investigations and incident response activities.

---

## Splunk_Search_Queries.txt

Contains all Splunk SPL queries used throughout the project.

Example queries include:

- Process Creation Detection
- File Create Detection
- ZIP Archive Detection
- IOC Extraction
- Event Investigation

These queries can be reused to reproduce the investigation and validate detection results.

---

# Detection Sources

- Microsoft Sysmon
- Windows Event Logs
- Splunk Enterprise

---

# Purpose

The purpose of these log files is to provide supporting evidence for the simulated data exfiltration investigation and demonstrate how Microsoft Sysmon and Splunk Enterprise can be used to detect, investigate, and analyze suspicious file collection and archive creation activities before a potential data exfiltration attempt.

---

# Note

This project is intended for educational purposes only.

No confidential information was accessed, transmitted, or exfiltrated during this project. All files used in this repository are dummy files created specifically for cybersecurity training and SOC analyst practice within a controlled lab environment.
