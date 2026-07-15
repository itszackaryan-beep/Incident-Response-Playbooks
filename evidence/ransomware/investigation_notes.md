# Investigation Report
# Investigation Notes

## Step 1 – Log Verification

### Objective
Verify that Windows Security Event Logs are being collected by Splunk.

### Observations
- Windows 7 Security Event Logs were successfully generated.
- Splunk received Windows Security logs successfully.
- Communication between Windows 7 and Splunk is working correctly.

### Evidence
- Screenshot 01: Splunk Security Logs
- Screenshot 02: Windows Event Viewer Security Logs
## Additional Evidence
- Screenshot 03 – Sysmon Download and Extract
- Screenshot 04 – Investigation Notes  

### Status
✅ Completed
---

## Evidence Screenshots

### Screenshot 01 - Splunk Security Logs
**Observation:**
- Splunk successfully received Windows Security Event Logs.
- Security events were indexed correctly without errors.


![Screenshot 02](screenshots/02_splunk_security_logs.jpg)

**Description:** Splunk successfully collected Windows Security Event Logs.

---

### Screenshot 02 - Windows Event Viewer Security Logs
**Observation:**
- Windows Security Event Viewer displayed successful log generation.
- Login and security events were available for analysis.

![Screenshot 01](screenshots/01_windows_security_event_viewer.jpg)

**Description:** Windows Event Viewer displaying Security logs generated during testing.

---

### Screenshot 03 - Sysmon Download and Extract
**Observation:**
- Sysmon package was successfully downloaded and extracted.
- The extracted files were ready for installation and endpoint monitoring configuration.


![Screenshot 03](screenshots/03_Sysmon_Download_and_Extract.jpg.png
)

**Description:** Sysmon downloaded and extracted for endpoint monitoring configuration.

---

### Screenshot 04 - Investigation Notes
**Observation:**
- Investigation findings were documented successfully.
- Log verification confirmed that Windows Security logs were collected by Splunk.
- The evidence was reviewed and the investigation step was marked as completed.

![Screenshot 04](screenshots/04_Sysmon_Operational_Logs.jpg)

**Description:** Final investigation notes documenting log verification and observations.
---
## Step 2 – Sysmon Installation and Configuration Verification

**Date:** (Today's Date)

### Objective
Verify that Microsoft Sysmon is successfully installed and configured on Windows Server 2022 for advanced endpoint monitoring and security event collection.

### Observations
- Microsoft Sysmon was successfully installed on Windows Server 2022.
- A custom Sysmon configuration file was applied successfully.
- The `Sysmon64` service was verified to be in the **RUNNING** state.
- Sysmon is actively monitoring endpoint activity and is ready to forward detailed telemetry for Splunk SIEM analysis.

### Evidence
- Screenshot 05: Sysmon Installation and Configuration Verification

### Status
✅ Completed

![Screenshot 05](screenshots/05_Sysmon_Operational_Log(1).jpg)

**Description:**
This screenshot confirms that Sysmon is successfully installed and actively generating operational events in Windows Event Viewer.

