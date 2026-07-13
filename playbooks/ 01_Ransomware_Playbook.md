# Ransomware Incident Response Playbook

## Markdown
## Table of Contents
1. Purpose
2. Scope
3. Roles and Responsibilities
4. Severity Classification
5. Detection Logic
6. Initial Triage
7. Containment Actions
8. Eradication Steps
9. Recovery Checklist
10. Indicators of Compromise (IOCs)
11. Communication Plan
12. Evidence Collection
13. Post-Incident Review
14. Lessons Learned
15. References
## 1. Purpose 
The purpose of this playbook is to provide a standardized and repeatable process for responding to ransomware incidents. It guides Security Operations Center (SOC) analysts through every stage of incident response, including detection, analysis, containment, eradication, recovery, and post-incident review. By following this playbook, organizations can minimize operational disruption, reduce the impact of ransomware attacks, protect critical assets, and improve their overall security posture while aligning with the NIST SP 800-61 Incident Response Framework.
## 2. Scope
This playbook is designed for handling ransomware incidents that impact an organization's IT environment. It applies to Windows workstations, servers, virtual machines, file servers, and other business-critical systems that may be targeted by ransomware.

The playbook is intended to support SOC analysts, incident responders, system administrators, and IT security teams during the incident response process. It provides clear guidance for identifying ransomware activity, containing the threat, removing malicious components, restoring affected systems, and documenting the incident. While this playbook follows the NIST SP 800-61 Incident Response Framework, it can be customized to align with an organization's internal security policies and operational procedures.
## 3. Roles and Responsibilities
| Role | Responsibilities |
|------|-------------------|
| **SOC Analyst (Tier 1)** | Monitor security alerts, validate ransomware indicators, perform initial triage, collect evidence, escalate confirmed incidents, and document findings. |
| **Incident Response Lead** | Coordinate the overall incident response process, assign tasks, communicate with stakeholders, and ensure that containment and recovery activities are completed effectively. |
| **System Administrator** | Isolate affected systems, disable compromised accounts if required, apply security patches, restore systems from clean backups, and verify that services are functioning normally. |
| **Threat Intelligence Analyst** | Identify indicators of compromise (IOCs), analyze ransomware behavior, map techniques to the MITRE ATT&CK framework, and provide threat intelligence to support the investigation. |
| **IT Manager / CISO** | Approve major response actions, coordinate business communication, manage external reporting requirements, and oversee the organization's recovery strategy. |
## 4. Severity Classification
| Severity | Description | Example |
|----------|-------------|---------|
| **Low** | A single endpoint is affected with no evidence of lateral movement or data loss. | One employee workstation infected. |
| **Medium** | Multiple endpoints are affected, but critical business services remain operational. | Several user devices encrypted within the same department. |
| **High** | A critical server or business application is compromised, causing significant operational disruption. | File server or database server encrypted by ransomware. |
| **Critical** | Widespread ransomware infection impacting multiple systems, business operations, or sensitive data across the organization. | Enterprise-wide ransomware outbreak affecting domain controllers and critical infrastructure. |
## 5. Detection Logic

Ransomware detection focuses on identifying suspicious activities that may indicate a ransomware attack. SOC analysts use security tools, system logs, and alerts to detect unusual behavior before the attack spreads further.

### Common Detection Indicators

- Sudden encryption of multiple files.
- Unusual file extensions added to documents.
- Ransom notes appearing on the system.
- Unknown or suspicious processes running.
- High CPU or disk activity caused by unknown applications.
- Attempts to delete backup files or shadow copies.
- Suspicious PowerShell or command-line activity.
- Antivirus or Endpoint Detection and Response (EDR) alerts.

### Windows Event Logs Used for Investigation

| Event ID | Purpose |
|----------|---------|
| 4688 | Used to monitor new process creation. |
| 7045 | Used to identify new services created on a system. |
| 5145 | Used to monitor network share access. |

### Example Splunk Query

```spl
index=windows EventCode=4688
```

This query helps analysts review process creation events and identify suspicious activity.

### MITRE ATT&CK Techniques

| Technique | ID | Description |
|-----------|----|-------------|
| Data Encrypted for Impact | T1486 | Attackers encrypt files to make them unavailable. |
| Inhibit System Recovery | T1490 | Attackers try to remove backups or recovery options. |

## 6. Initial Triage

Initial triage is the first step performed after detecting a suspected ransomware incident. The main goal of triage is to confirm the incident, understand the impact, and collect important information before taking containment actions.

### Triage Steps

1. **Identify the Affected System**
   - Record the hostname, IP address, operating system, and location of the affected device.
   - Identify whether the system is a workstation, server, or critical asset.

2. **Identify the User and Account Activity**
   - Determine the user account involved.
   - Check recent login activity and suspicious account behavior.

3. **Verify Ransomware Indicators**
   - Check for encrypted files, ransom notes, unusual file extensions, and suspicious processes.
   - Confirm whether the activity matches ransomware behavior.

4. **Collect Initial Evidence**
   - Collect relevant logs, alerts, screenshots, and suspicious file information.
   - Preserve evidence for further investigation.

5. **Determine the Scope of Impact**
   - Check if other systems are affected.
   - Identify possible lateral movement or network spread.

6. **Assign Incident Severity**
   - Classify the incident as Low, Medium, High, or Critical based on the impact and number of affected systems.

### Information to Collect

| Information | Purpose |
|-------------|---------|
| Hostname | Identify the affected machine |
| IP Address | Track network activity |
| Username | Identify affected account |
| Detection Time | Build incident timeline |
| Malware/File Name | Support investigation |
| Logs and Alerts | Analyze attack activity |
## 7. Containment Actions

Containment is the process of limiting the spread and impact of a ransomware attack. The main objective is to isolate affected systems, prevent further damage, and stop the attacker from gaining additional access.

### Immediate Containment Actions

1. **Isolate the Affected System**
   - Disconnect the infected system from the network.
   - Disable Wi-Fi or remove network access to prevent ransomware spread.

2. **Disable Compromised Accounts**
   - Temporarily disable user accounts suspected of being compromised.
   - Reset passwords if unauthorized access is confirmed.

3. **Block Malicious Activity**
   - Block suspicious IP addresses, domains, or communication channels.
   - Prevent communication between infected systems and attacker infrastructure.

4. **Stop Malicious Processes**
   - Identify and stop suspicious processes related to ransomware activity.
   - Prevent further file encryption or system modification.

5. **Protect Critical Systems**
   - Isolate important servers and business-critical systems.
   - Review network shares and restrict unnecessary access.

### Containment Checklist

| Action | Status |
|--------|--------|
| Affected device isolated | ☐ |
| Compromised accounts disabled | ☐ |
| Malicious IPs/domains blocked | ☐ |
| Suspicious processes stopped | ☐ |
| Security team notified | ☐ |

The containment phase should be completed quickly to reduce the impact of the ransomware attack and prevent further compromise.
## 8. Eradication Steps

Eradication is the process of removing the ransomware infection from affected systems and eliminating the root cause that allowed the attack to occur. The goal is to ensure that the attacker no longer has access and the system is safe for recovery.

### Eradication Steps

1. **Remove Malicious Files**
   - Identify and remove ransomware executables, scripts, and suspicious files.
   - Verify that no malicious files remain on the affected system.

2. **Remove Persistence Mechanisms**
   - Check for suspicious startup programs, scheduled tasks, and unauthorized services.
   - Remove any persistence methods created by the attacker.

3. **Perform Security Scanning**
   - Run antivirus and Endpoint Detection and Response (EDR) scans.
   - Analyze detected threats and confirm removal.

4. **Reset Compromised Credentials**
   - Reset passwords for affected user accounts.
   - Review privileged accounts for suspicious activity.

5. **Patch Security Vulnerabilities**
   - Install missing security updates and patches.
   - Fix vulnerabilities that may have been exploited by attackers.

6. **Verify System Integrity**
   - Confirm that system files and security controls are working properly.
   - Ensure the system is clean before moving to the recovery phase.

### Eradication Checklist

| Action | Status |
|--------|--------|
| Malware files removed | ☐ |
| Persistence mechanisms removed | ☐ |
| Security scans completed | ☐ |
| Passwords reset | ☐ |
| Vulnerabilities patched | ☐ |
| System verified as clean | ☐ |

Successful eradication ensures that the ransomware threat has been removed and the environment is ready for recovery.
## 9. Recovery Checklist

Recovery is the process of restoring affected systems and services back to normal operations after removing the ransomware infection. The main goal is to safely recover business operations while ensuring that the environment is secure.

### Recovery Steps

1. **Restore Systems from Clean Backups**
   - Recover encrypted files and systems using verified clean backups.
   - Ensure backups are not affected by ransomware before restoration.

2. **Validate System Functionality**
   - Confirm that restored systems and applications are working properly.
   - Verify that important files and services are available.

3. **Enable Security Monitoring**
   - Monitor restored systems for any signs of suspicious activity.
   - Continue reviewing security alerts and logs.

4. **Reset User Access**
   - Confirm that user accounts are secure.
   - Re-enable accounts only after completing security checks.

5. **Update Security Controls**
   - Review antivirus, firewall, and endpoint security configurations.
   - Apply additional security measures to prevent future incidents.

6. **Return Systems to Production**
   - Gradually reconnect systems to the network.
   - Confirm normal business operations have resumed.

### Recovery Checklist

| Action | Status |
|--------|--------|
| Backup integrity verified | ☐ |
| Data restored successfully | ☐ |
| Applications tested | ☐ |
| User access reviewed | ☐ |
| Security monitoring enabled | ☐ |
| Systems returned to normal operation | ☐ |

After recovery, continuous monitoring should be performed to ensure that ransomware does not return and no hidden threats remain in the environment.
## 10. Indicators of Compromise (IOCs)

Indicators of Compromise (IOCs) are evidence or signs that help security analysts identify and investigate ransomware activity. SOC analysts use these indicators during threat detection, investigation, and incident response.

### Common Ransomware IOCs

| IOC Type | Description | Example |
|----------|-------------|---------|
| File Extensions | New file extensions added after encryption | .locked, .encrypted, .crypt |
| Suspicious Files | Unknown ransomware-related files found on the system | malicious.exe, ransom_note.txt |
| Processes | Unusual processes running on the endpoint | unknown executable, suspicious PowerShell process |
| Network Activity | Communication with suspicious external servers | Unknown IP addresses or domains |
| Registry Changes | Unauthorized modifications used for persistence | Suspicious startup entries |
| User Activity | Abnormal login or account behavior | Unusual account access |

### Evidence Collected During Investigation

- Malware file hashes
- Suspicious IP addresses
- Malicious domains
- File names related to ransomware
- Ransom notes
- System logs
- Process information
- Network connection details

### IOC Handling Process

1. Collect suspicious indicators from affected systems.
2. Analyze indicators using security tools.
3. Block confirmed malicious indicators.
4. Share relevant IOCs with the security team.
5. Monitor the environment for similar activity.

## 11. Communication Plan

Effective communication is an important part of incident response. During a ransomware incident, the security team must share accurate information with the right stakeholders to ensure quick decision-making and proper coordination.

### Communication Process

| Team / Role | Responsibility |
|-------------|----------------|
| **SOC Analyst** | Report the detected ransomware activity, provide investigation findings, and update incident status. |
| **Incident Response Team** | Coordinate response activities, manage containment actions, and track incident progress. |
| **System Administrator** | Assist with system isolation, recovery activities, and technical remediation. |
| **IT Manager / Management** | Make business decisions, approve major actions, and coordinate organizational response. |
| **Affected Users** | Follow security instructions and provide required information about the incident. |

### Communication Guidelines

- Report confirmed ransomware incidents immediately to the incident response team.
- Maintain proper documentation of all communication and actions taken.
- Share only verified information to avoid confusion.
- Provide regular updates until the incident is resolved.
- Conduct a final incident report after recovery is completed.

### Communication Channels

- Security incident management system
- Email notifications
- Internal communication platforms
- Emergency response meetings

Proper communication helps reduce response time, improves coordination, and ensures that all teams work together during a ransomware incident.
## 12. Evidence Collection

Evidence collection is an important step during a ransomware investigation. The purpose of collecting evidence is to understand how the attack occurred, identify affected systems, analyze attacker activity, and support future security improvements.

### Evidence to Collect

| Evidence Type | Description |
|---------------|-------------|
| **System Logs** | Collect Windows Event Logs, security logs, and application logs from affected systems. |
| **Security Alerts** | Gather alerts generated by antivirus, EDR, SIEM, or monitoring tools. |
| **Suspicious Files** | Collect ransomware samples, malicious files, and ransom notes for analysis. |
| **Process Information** | Record running processes, suspicious applications, and executed commands. |
| **Network Data** | Collect firewall logs, network connections, and communication details with external systems. |
| **User Activity Logs** | Review login attempts, account activity, and privilege changes. |
| **File Information** | Document encrypted files, file extensions, timestamps, and affected directories. |

### Evidence Handling Guidelines

- Preserve original evidence without modification.
- Record the date, time, and source of collected evidence.
- Store evidence securely with proper access control.
- Maintain documentation of all investigation activities.
- Follow proper evidence handling procedures.

Proper evidence collection helps SOC analysts perform accurate investigations and identify the root cause of the ransomware incident.
## 13. Post-Incident Review

The post-incident review is conducted after resolving the ransomware incident to analyze what happened, how it was handled, and how future incidents can be prevented.

### Review Points

- Identify the root cause of the ransomware attack.
- Review the response actions taken by the security team.
- Document what worked well and what needs improvement.
- Update security controls and incident response procedures.

A proper post-incident review helps improve the organization's security and prepares the team for future threats.
## 14. Lessons Learned

Lessons learned help the security team improve their response process and reduce the risk of future ransomware attacks.

### Key Improvements

- Identify security gaps and weaknesses.
- Improve monitoring and detection capabilities.
- Provide security awareness training to users.
- Update incident response procedures based on findings.

Continuous improvement helps organizations build stronger security defenses.

## 15. References

- NIST SP 800-61: Computer Security Incident Handling Guide
- MITRE ATT&CK Framework
- Microsoft Security Documentation
