===========================================================
Data Exfiltration Detection
Splunk Search Queries
===========================================================

===========================================================
1. Process Creation Detection
===========================================================

index=soc_lab EventCode=1

Purpose:
Detect Microsoft Sysmon Process Creation events.

-----------------------------------------------------------

===========================================================
2. File Create Detection
===========================================================

index=soc_lab EventCode=11

Purpose:
Detect file creation activities including confidential files,
temporary staging folder, and ZIP archive creation.

-----------------------------------------------------------

===========================================================
3. Process and File Activity Investigation
===========================================================

index=soc_lab (EventCode=1 OR EventCode=11)
| table _time host User Image TargetFilename EventCode

Purpose:
Display important investigation fields in a tabular format.

-----------------------------------------------------------

===========================================================
4. ZIP Archive Detection
===========================================================

index=soc_lab TargetFilename="*Collected_Data.zip*"

Purpose:
Identify the creation of the compressed archive used during
the simulated data staging process.

-----------------------------------------------------------

===========================================================
5. Company Data Folder Investigation
===========================================================

index=soc_lab TargetFilename="*Company_Data*"

Purpose:
Verify creation of the simulated confidential company folder.

-----------------------------------------------------------

===========================================================
6. Temporary Staging Folder Investigation
===========================================================

index=soc_lab TargetFilename="*Collected_Data*"

Purpose:
Detect the temporary staging directory and copied files.

-----------------------------------------------------------

===========================================================
7. IOC Extraction
===========================================================

index=soc_lab (EventCode=1 OR EventCode=11)
| table _time host User Image TargetFilename EventCode

Purpose:
Extract Indicators of Compromise (IOCs) for forensic analysis.

-----------------------------------------------------------

===========================================================
8. Event Statistics
===========================================================

index=soc_lab (EventCode=1 OR EventCode=11)
| stats count by EventCode

Purpose:
Display the total number of Process Create and File Create
events generated during the investigation.

-----------------------------------------------------------

===========================================================
9. Timeline View
===========================================================

index=soc_lab (EventCode=1 OR EventCode=11)
| sort _time

Purpose:
Reconstruct the sequence of events during the simulated
data staging activity.

-----------------------------------------------------------

===========================================================
End of Search Queries
===========================================================
