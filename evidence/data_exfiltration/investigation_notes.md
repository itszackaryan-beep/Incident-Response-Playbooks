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
![Screenshot 00](screenshots/00_Lab_Connectivity.jpg.jpg)
---

## Screenshot 01 – Microsoft Sysmon Verification

**Filename**

```text
01_Sysmon_Service.jpg
```

**Description**

Shows Microsoft Sysmon service running successfully on Windows Server 2022.

> 📸 Place Screenshot Here
![Screenshot 01](screenshots/01_Sysmon_Service.jpg.jpg)
---

## Screenshot 02 – Splunk Log Collection Verification

**Filename**

```text
02_Splunk_Receiving_Logs.jpg
```

**Description**

Shows Splunk Enterprise successfully receiving Windows Sysmon events.

> 📸 Place Screenshot Here
![Screenshot 02](screenshots/02_Splunk_Receiving_Logs.jpg.jpg)
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
index=main EventCode=1
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

# Step 1 – Sensitive Company Data Creation

## Objective

Create a set of simulated confidential company files that will be used during the Data Exfiltration Detection investigation.

---

## Background

One of the earliest stages of a data exfiltration attack involves identifying and collecting valuable organizational data such as employee records, financial reports, customer databases, and confidential documents.

In this lab, a safe simulation is performed by creating dummy files that represent sensitive company information. No real confidential data is used.

---

## Tasks Performed

- Created a folder named **Company_Data**.
- Generated multiple dummy confidential files.
- Stored all files inside the Company_Data folder.
- Verified the files were successfully created.
- Prepared the environment for the next stage of the investigation.

---

# Folder Location

```text
C:\Company_Data
```

---

# Sample Files Created

```text
Employee_Salary.xlsx
Employee_Details.xlsx
Customer_Database.csv
Financial_Report_2026.xlsx
HR_Records.docx
Confidential_Project.pdf
```

---

## Observations

- The Company_Data folder was created successfully.
- Six dummy confidential files were generated.
- The files simulate sensitive organizational information.
- These files will be used during the simulated data collection phase.

---

# Evidence

## Screenshot 03 – Company Data Folder

**Filename**

```text
03_Company_Data_Folder.jpg
```

**Description**

Shows the Company_Data folder created successfully on Windows Server.

> 📸 Place Screenshot Here
![Screenshot 03](screenshots/03_Company_Data_Folder.jpg.jpg)
---

## Screenshot 04 – Confidential Files

**Filename**

```text
04_Confidential_Files.jpg
```

**Description**

Displays all simulated confidential company files inside the Company_Data folder.

> 📸 Place Screenshot Here
![Screenshot 04](screenshots/04_Confidential_Files.jpg.jpg)
---

## Result

The simulated confidential company data was successfully created and prepared for the Data Exfiltration Detection investigation.

---

## Status

✅ Completed

# Step 2 – Data Collection (Data Staging)

## Objective

Simulate the collection of sensitive company files into a temporary staging folder and verify that Microsoft Sysmon records the associated file activity.

---

## Background

Before exfiltrating data, attackers commonly collect important files into a temporary location. This process is known as **Data Staging**.

By staging files in one directory, attackers can easily compress, archive, or prepare them for transfer.

In this lab, a safe simulation is performed by copying dummy confidential files into a temporary folder. No files leave the Windows Server and no actual data exfiltration occurs.

---

## Tasks Performed

- Created a temporary folder named **Collected_Data**.
- Copied all simulated confidential files from **Company_Data**.
- Stored the copied files inside the Collected_Data folder.
- Verified that Microsoft Sysmon generated File Create events.
- Confirmed that Splunk Enterprise successfully collected the generated logs.

---

## Source Folder

```text
C:\Company_Data
```

## Destination Folder

```text
C:\Temp\Collected_Data
```

---

## Files Copied

```text
Employee_Salary.xlsx
Employee_Details.xlsx
Customer_Database.csv
Financial_Report_2026.xlsx
HR_Records.docx
Confidential_Project.pdf
```

---

## Observations

- The Collected_Data folder was created successfully.
- All dummy confidential files were copied successfully.
- Microsoft Sysmon generated File Create (Event ID 11) events.
- Splunk Enterprise successfully indexed the generated file activity.
- The activity simulates the data staging phase commonly observed before data exfiltration.

---

# Evidence

## Screenshot 05 – Data Collection Folder

**Filename**

```text
05_Data_Collection_Folder.jpg
```

**Description**

Shows the Collected_Data folder containing the copied confidential files.

> 📸 Place Screenshot Here
![Screenshot 05](screenshots/05_Data_Collection_Folder.jpg.jpg)
---

## Screenshot 06 – File Activity Detection in Splunk

**Filename**

```text
06_File_Activity_Detection_Splunk.jpg
```

**Description**

Shows Microsoft Sysmon File Create (Event ID 11) events generated during the file copy operation.

> 📸 Place Screenshot Here
![Screenshot 06](screenshots/06_File_Activity_Detection_Splunk.jpg.jpg)
---

## SPL Query

```spl
index=soc_lab EventCode=11
```

Alternative

```spl
index=main EventCode=11
```

---

## Result

The confidential files were successfully collected into a temporary staging folder. Microsoft Sysmon detected the file creation activity, and Splunk Enterprise successfully indexed the generated events. This demonstrates how defenders can identify data staging activity before a potential data exfiltration attempt.

---

## Status

✅ Completed

# Step 3 – Archive Creation (Data Staging)

## Objective

Simulate an attacker preparing collected files for exfiltration by compressing them into a ZIP archive and verify that Microsoft Sysmon records the file creation activity.

---

## Background

Before data is transferred outside an organization, attackers often compress multiple files into a single archive. This reduces file size, keeps related documents together, and makes data transfer easier.

In this lab, a safe simulation is performed by creating a ZIP archive containing dummy company files. No data is transmitted outside the lab environment.

---

## Tasks Performed

- Opened the **Collected_Data** folder.
- Selected all collected dummy files.
- Created a ZIP archive named **Collected_Data.zip**.
- Verified that the ZIP file was created successfully.
- Confirmed that Microsoft Sysmon generated file creation events.
- Verified that Splunk Enterprise collected the generated logs.

---

## Archive Location

```text
C:\Temp\Collected_Data\Collected_Data.zip
```

---

## Observations

- The ZIP archive was successfully created.
- Microsoft Sysmon detected the archive creation activity.
- Splunk Enterprise successfully indexed the generated events.
- Archive creation represents the data staging phase before exfiltration.

---

# Evidence

## Screenshot 06 – ZIP Archive Created

**Filename**

```text
06_ZIP_Archive_Created.jpg
```

**Description**

Shows the Collected_Data.zip archive successfully created inside the Collected_Data folder.

> 📸 Place Screenshot Here
![Screenshot 06](screenshots/06_ZIP_Archive_Created.jpg.jpg)
---

## Screenshot 07 – ZIP File Detection in Splunk

**Filename**

```text
07_ZIP_File_Detection_Splunk.jpg
```

**Description**

Shows Microsoft Sysmon Event ID 11 related to the ZIP archive creation.

> 📸 Place Screenshot Here
![Screenshot 06](screenshots/07_ZIP_File_Detection_Splunk.jpg.jpg)
---

## SPL Query

```spl
index=soc_lab EventCode=11
```

Alternative

```spl
index=main EventCode=11
```

---

## Result

The ZIP archive was successfully created and Microsoft Sysmon recorded the associated file creation activity. Splunk Enterprise successfully indexed the event, demonstrating how data staging activities can be monitored before a potential data exfiltration attempt.

---

## Status

✅ Completed
