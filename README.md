# wazuh-threat-hunting-lab21-windows-lnk-artifact-investigation
## Overview

Windows Shortcut (LNK) files are important forensic artifacts that help investigators determine which files or applications a user accessed. During DFIR investigations, LNK artifacts can provide evidence of user activity even if the original file has been moved or deleted.

In this lab, recently accessed documents were examined using Windows Shortcut artifacts and correlated with Sysmon Event ID 1 (Process Creation) and Wazuh Threat Hunting to reconstruct user activity.

---

# Lab Objectives

- Understand the purpose of Windows Shortcut (LNK) artifacts
- Simulate normal user document access
- Locate recently accessed shortcut files
- Examine shortcut properties
- Investigate Sysmon Process Creation events
- Correlate evidence using Wazuh
- Build a forensic timeline

---

# Lab Environment

## Endpoint

- Windows 11

## Monitoring

- Wazuh Agent
- Wazuh Manager
- Sysmon

## Tools

- PowerShell
- Windows Explorer
- Notepad
- Wazuh Dashboard

---

# Why LNK Artifacts Matter

Windows creates shortcut (.lnk) files to improve user experience and maintain references to recently accessed files.

From a DFIR perspective, these artifacts help investigators answer questions such as:

- Which document was opened?
- Which application opened it?
- Where was the original file located?
- When was it accessed?
- Can user activity be reconstructed?

Even if the original file is deleted, LNK artifacts may still provide valuable evidence during an investigation.

---

# Investigation Workflow

```
Create Documents
        ↓
User Opens Documents
        ↓
Notepad Launches
        ↓
Windows Updates Recent Items
        ↓
Sysmon Event ID 1
        ↓
Wazuh Collects Telemetry
        ↓
DFIR Investigation
```

---

# Investigation Steps

1. Verify Sysmon and Wazuh services.
2. Create sample confidential documents.
3. Open each document using Notepad.
4. Inspect the Recent Items folder for LNK artifacts.
5. Review shortcut properties.
6. Investigate Sysmon Event ID 1.
7. Hunt process creation events in Wazuh.
8. Correlate all evidence into a timeline.

---

# Wazuh Queries

## Process Creation

```
data.win.system.eventID:1
```

## Process Name

```
notepad.exe
```

---

# MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---------|-----------|----|
| Execution | User Execution | T1204 |
| Collection | Data from Local System | T1005 |

---

# Investigation Summary

Three confidential documents were created and opened using Notepad. Windows generated recent item shortcut (LNK) artifacts while Sysmon captured Notepad process execution. Wazuh successfully ingested the endpoint telemetry, allowing user activity to be reconstructed by correlating Windows forensic artifacts with endpoint logs.

---

# Skills Demonstrated

- Windows DFIR
- LNK Artifact Analysis
- User Activity Investigation
- Sysmon Analysis
- Wazuh Threat Hunting
- Timeline Reconstruction
- Digital Forensics
- SOC Investigation

---

# Learning Outcome

This lab demonstrates how Windows Shortcut artifacts complement endpoint telemetry during forensic investigations. By combining LNK artifacts with Sysmon Process Creation events and Wazuh Threat Hunting, investigators can validate document access and reconstruct user activity with greater confidence.
