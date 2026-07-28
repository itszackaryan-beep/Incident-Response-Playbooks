# Investigation Notes

> This file will be updated after completing the practical investigation.

# Brute Force Attack Investigation Report

## Step 1 – Failed Login Simulation

### Objective

Simulate multiple failed Windows login attempts and verify that Windows Security logs are collected by Splunk Enterprise.

---

### Background

A brute force attack is a technique where an attacker repeatedly attempts different passwords until the correct one is found. Windows records these failed authentication attempts as **Event ID 4625** in the Security Event Log.

This lab performs a **safe simulation** by intentionally generating failed login attempts without using any attack tools.

---

### Tasks Performed

- Generated multiple failed Windows login attempts.
- Verified Windows Security **Event ID 4625**.
- Confirmed that Splunk Enterprise successfully indexed the generated events.

---

### Observations

- Multiple failed login attempts were generated successfully.
- Windows Security Event ID **4625** was recorded.
- Splunk Enterprise successfully collected the authentication events.
- The generated logs can be used to detect brute force attacks.

---

## Evidence

### Screenshot 01 – Failed Login Attempts

Shows multiple failed login attempts generated on the Windows system.

**Filename**

```
01_Failed_Login_Attempts.jpg
```

---

### Screenshot 02 – Failed Login Events in Splunk

Displays Windows Security **Event ID 4625** collected by Splunk Enterprise.

**Filename**

```
02_EventID4625_in_Splunk.jpg
```

---

### SPL Query

```spl
index=main EventCode=4625
```

---

### Result

Windows Security successfully generated failed authentication events and Splunk Enterprise indexed the logs for investigation.

---

## Status

✅ Completed

---

# Step 2 – Successful Login Verification

## Objective

Verify that a successful login event is recorded after the failed login attempts.

---

## Tasks Performed

- Logged in using the correct credentials.
- Verified Windows Security **Event ID 4624**.
- Confirmed successful log collection in Splunk Enterprise.

---

## Observations

- Successful authentication was recorded.
- Windows generated Event ID **4624**.
- Splunk successfully indexed the event.

---

## Evidence

### Screenshot 03 – Successful Login Event

Shows Windows Security **Event ID 4624**.

**Filename**

```
03_Successful_Login_Event.jpg
```

---

### Screenshot 04 – Successful Login in Splunk

Displays Event ID **4624** in Splunk Enterprise.

**Filename**

```
04_EventID4624_in_Splunk.jpg
```

---

### SPL Query

```spl
index=main EventCode=4624
```

---

## Result

Successful authentication events were detected and indexed correctly.

---

## Status

✅ Completed

---

# Step 3 – Brute Force Investigation

## Objective

Investigate repeated failed login attempts using Splunk Enterprise.

---

## Tasks Performed

- Searched Event ID **4625**.
- Counted failed authentication attempts.
- Reviewed affected user accounts.

---

## Observations

- Multiple failed login events were detected.
- Repeated authentication failures indicate brute force activity.

---

## Evidence

### Screenshot 05 – Multiple Failed Login Events

**Filename**

```
05_Multiple_Failed_Login_Events.jpg
```

---

### Screenshot 06 – Failed Login Statistics

**Filename**

```
06_Failed_Login_Statistics.jpg
```

---

### SPL Queries

```spl
index=main EventCode=4625
```

```spl
index=main EventCode=4625
| stats count by Account_Name
```

---

## Result

Repeated failed authentication attempts were identified successfully.

---

## Status

✅ Completed

---

# Step 4 – IOC Extraction

## Objective

Extract Indicators of Compromise (IOCs) from the collected authentication logs.

---

## IOC Information

- Host Name
- Username
- Event ID
- Logon Type
- Source IP Address (if available)
- Timestamp

---

## Evidence

### Screenshot 07 – IOC Extraction Query

**Filename**

```
07_IOC_Extraction_Query.jpg
```

---

### Screenshot 08 – IOC Table

**Filename**

```
08_IOC_Table.jpg
```

---

### SPL Query

```spl
index=main (EventCode=4624 OR EventCode=4625)
| table _time host Account_Name Source_Network_Address Logon_Type EventCode
```

---

## Result

Authentication-related IOCs were successfully extracted.

---

## Status

✅ Completed

---

# Step 5 – Incident Timeline

## Objective

Create a timeline of the brute force attack simulation.

| Time | Activity |
|------|----------|
|10:20|Failed Login Attempt #1|
|10:21|Failed Login Attempt #2|
|10:22|Failed Login Attempt #3|
|10:23|Successful Login|
|10:24|Splunk Investigation|

---

## Evidence

### Screenshot 09 – Incident Timeline

**Filename**

```
09_Incident_Timeline.jpg
```

---

## Status

✅ Completed

---

# Step 6 – MITRE ATT&CK Mapping

## Objective

Map the observed activity to the MITRE ATT&CK framework.

| Activity | Technique ID | Technique |
|-----------|--------------|-----------|
| Password Guessing | T1110.001 | Password Guessing |

---

## Evidence

### Screenshot 10 – MITRE ATT&CK Mapping

**Filename**

```
10_MITRE_ATTACK_Mapping.jpg
```

---

## Status

✅ Completed

---

# Step 7 – Incident Response Summary

## Detection

Splunk detected repeated Windows authentication failures (Event ID 4625).

---

## Analysis

The investigation identified multiple failed login attempts followed by a successful authentication event.

---

## Containment

- Monitor repeated failed logins.
- Lock affected accounts if necessary.
- Enable account lockout policies.

---

## Eradication

- Reset compromised passwords.
- Review authentication logs.
- Verify account integrity.

---

## Recovery

- Restore secure user access.
- Continue monitoring authentication events.

---

## Lessons Learned

- Windows Security logs provide valuable authentication evidence.
- Splunk Enterprise effectively detects brute force activity.
- Monitoring Event IDs 4624 and 4625 improves threat detection.

---

## Evidence

### Screenshot 11 – Incident Response Summary

**Filename**

```
11_Incident_Response_Summary.jpg
```

---

# Conclusion

The brute force attack simulation successfully demonstrated how Windows Security Event Logs and Splunk Enterprise can detect and investigate repeated authentication failures. The project covered failed logins, successful authentication, IOC extraction, timeline analysis, MITRE ATT&CK mapping, and incident response using a safe lab environment.

---

# Status

## ✅ Project Completed
