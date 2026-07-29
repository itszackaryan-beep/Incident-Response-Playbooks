# DATA EXFILTRATION
## Investigation Notes

# Step 0 – Lab Setup

## Objective

Prepare the cybersecurity lab environment for a safe Data Exfiltration Detection and Investigation simulation using Microsoft Sysmon and Splunk Enterprise.

---

## Background

Before beginning the investigation, all lab components must be verified to ensure proper communication and log collection.

The objective of this step is to confirm that Windows Server 2022, Kali Linux, Microsoft Sysmon, and Splunk Enterprise are functioning correctly and ready for the data exfiltration simulation.

No malicious activity is performed during this stage.

---

## Lab Environment

| Component | Version |
|-----------|----------|
| Hypervisor | VMware Workstation |
| Operating System | Windows Server 2022 |
| Attacker Machine | Kali Linux 2026.1 |
| SIEM | Splunk Enterprise |
| Endpoint Monitoring | Microsoft Sysmon |

---

## Tasks Performed

- Started Windows Server 2022 virtual machine.
- Started Kali Linux virtual machine.
- Verified both systems were connected to the same VMware NAT network.
- Confirmed successful connectivity using ICMP (ping).
- Verified Microsoft Sysmon service was running.
- Confirmed Splunk Enterprise was receiving Windows Sysmon events.

---

# Evidence

## Screenshot 00 – Lab Connectivity Verification

**Filename**

```text
00_Lab_Connectivity.jpg
```

**Description**

Shows successful network connectivity between Kali Linux and Windows Server 2022 using the ping command.

> 📸 Place Screenshot Here

---

## Screenshot 01 – Microsoft Sysmon Verification

**Filename**

```text
01_Sysmon_Service.jpg
```

**Description**

Shows Microsoft Sysmon service running successfully on Windows Server 2022.

> 📸 Place Screenshot Here

---

## Screenshot 02 – Splunk Log Collection Verification

**Filename**

```text
02_Splunk_Receiving_Logs.jpg
```

**Description**

Shows Splunk Enterprise successfully receiving Windows Sysmon events.

> 📸 Place Screenshot Here

---

# Commands Used

### Kali Linux

```bash
ping <Windows_Server_IP>
```

Example

```bash
ping 192.168.xxx.xxx
```

---

### Windows Server

```cmd
hostname
```

```cmd
ipconfig
```

---

### Splunk Search

```spl
index=soc_lab EventCode=1
```

or

```spl
index=soc_lab
```

---

## Observations

- Windows Server and Kali Linux communicated successfully.
- Microsoft Sysmon was actively monitoring endpoint events.
- Splunk Enterprise successfully collected Sysmon logs.
- The lab environment was ready for the Data Exfiltration simulation.

---

## Result

The lab environment was successfully configured for the Data Exfiltration Detection project. All systems were operational, endpoint monitoring was enabled, and Splunk Enterprise was successfully receiving Windows Sysmon events.

---

## Status

✅ Completed
> This file will be updated after completing the practical investigation.
