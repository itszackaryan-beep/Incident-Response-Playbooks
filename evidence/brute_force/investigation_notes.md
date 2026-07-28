# Investigation Notes

> This file will be updated after completing the practical investigation.

# Step 0 – Lab Setup and Connectivity Verification

## Objective

Verify that the attacker machine (Kali Linux) and the target machine (Windows Server 2022) are properly connected over the VMware virtual network before performing the brute force attack simulation.

---

## Background

Before any authentication testing, it is important to verify that both virtual machines can communicate with each other. Proper network connectivity ensures that Windows Security logs and Splunk Enterprise can accurately capture authentication events generated during the investigation.

This step validates the lab environment and confirms that Remote Desktop Protocol (RDP) is available for authentication testing.

---

## Lab Environment

| Component | Description |
|-----------|-------------|
| Hypervisor | VMware Workstation |
| Attacker Machine | Kali Linux |
| Target Machine | Windows Server 2022 |
| SIEM | Splunk Enterprise |
| Log Source | Windows Security Event Logs |
| Network Mode | NAT |

---

## Tasks Performed

- Verified that Kali Linux and Windows Server 2022 were connected to the same VMware NAT network.
- Confirmed IP connectivity using the **ping** command.
- Enabled Remote Desktop (RDP) on Windows Server 2022.
- Verified that TCP Port **3389** was in the **LISTENING** state.
- Confirmed that the lab environment was ready for authentication testing.

---

## Observations

- VMware networking was configured successfully.
- Kali Linux successfully communicated with Windows Server 2022.
- Windows Server responded to ICMP (Ping) requests.
- Remote Desktop service was enabled successfully.
- TCP Port 3389 was listening for incoming RDP connections.
- The environment was ready for brute force authentication simulation.

---

# Evidence

## Screenshot 00 – Kali Linux Connectivity Verification

**Filename**

```text
00_Kali_RDP_Connectivity.jpg
```

**Description**

Kali Linux successfully communicating with Windows Server 2022 using network connectivity verification (Ping).

---

## Screenshot 01 – Remote Desktop Enabled

**Filename**

```text
01_Remote_Desktop_Enabled.jpg
```

**Description**

Windows Server 2022 showing Remote Desktop enabled for incoming RDP connections.

---

## Screenshot 02 – RDP Service Listening

**Filename**

```text
02_RDP_Port_3389_LISTENING.jpg
```

**Description**

Command Prompt displaying TCP Port 3389 in the LISTENING state, confirming that the Remote Desktop service is active.

---

## Commands Used

### Windows Server

```cmd
ipconfig
```

```cmd
netstat -an | find "3389"
```

### Kali Linux

```bash
ping <Windows_Server_IP>
```

---

## Result

The attacker machine (Kali Linux) and the target machine (Windows Server 2022) were successfully connected over the VMware NAT network. Remote Desktop was enabled and verified, confirming that the environment was fully prepared for the brute force authentication simulation.

---

## Status

✅ Completed
# Step 1 – Failed Login Simulation

## Objective

Simulate multiple failed Windows login attempts and verify that Windows Security Event ID **4625** is generated and successfully collected by Splunk Enterprise.

---

## Background

A brute force attack involves repeatedly attempting different passwords to gain unauthorized access to a user account. Windows records every failed authentication attempt as **Security Event ID 4625**.

In this lab, a **safe simulation** is performed by intentionally entering incorrect credentials through Remote Desktop Protocol (RDP). No password cracking tools or malicious software are used.

---

## Lab Components

| Component | Description |
|-----------|-------------|
| Attacker Machine | Kali Linux |
| Target Machine | Windows Server 2022 |
| SIEM | Splunk Enterprise |
| Event ID | 4625 (Failed Logon) |

---

## Tasks Performed

- Established an RDP connection from Kali Linux to Windows Server 2022.
- Entered an incorrect password **5–10 times** for the Administrator account.
- Verified that Windows Security generated **Event ID 4625**.
- Confirmed that Splunk Enterprise successfully indexed the failed authentication events.

---

## Observations

- Multiple failed login attempts were generated successfully.
- Windows Security recorded Event ID **4625** for each failed authentication attempt.
- Splunk Enterprise successfully received and indexed the authentication logs.
- The generated events can be used to identify brute force attack activity.

---

# Evidence

## Screenshot 03 – RDP Login Attempt from Kali Linux

**Filename**

```text
03_RDP_Login_Attempt_From_Kali.jpg
```

**Description**

Kali Linux initiating a Remote Desktop connection to Windows Server 2022 for authentication testing.

---

## Screenshot 04 – Failed Login Message

**Filename**

```text
04_Failed_Login_Message.jpg
```

**Description**

Windows Server displaying an authentication failure after an incorrect password was entered.

---

## Screenshot 05 – Event ID 4625 in Event Viewer

**Filename**

```text
05_EventID4625_EventViewer.jpg
```

**Description**

Windows Security Event Viewer displaying Event ID 4625 generated during the failed login attempts.

---

## Screenshot 06 – Event ID 4625 in Splunk

**Filename**

```text
06_EventID4625_in_Splunk.jpg
```

**Description**

Splunk Enterprise displaying Windows Security Event ID 4625 collected from Windows Server 2022.

---

## SPL Query

```spl
index=main EventCode=4625
```

If your Windows Security logs are stored in another index:

```spl
index=soc_lab EventCode=4625
```

---

## Result

The failed authentication attempts successfully generated Windows Security Event ID 4625. Splunk Enterprise collected and indexed the events, confirming that the SIEM environment can detect brute force login attempts.

---

## Status

⬜ Pending
