# Investigation Notes

## Incident Summary

The investigation focused on determining whether confidential documents had been accessed by a user.

Windows Shortcut (LNK) artifacts, Sysmon process creation events, and Wazuh telemetry were correlated to reconstruct user activity.

---

# Investigation Timeline

## Step 1

Verified monitoring services.

Observed

- Sysmon Service Running
- Wazuh Agent Running

---

## Step 2

Created investigation documents.

Files Created

- Confidential1.txt
- Confidential2.txt
- Confidential3.txt

Location

```
C:\LNKLab
```

---

## Step 3

Opened each document using Windows Explorer.

Observed

- Explorer launched Notepad.
- Each document was viewed briefly.
- User activity generated endpoint telemetry.

---

## Step 4

Inspected Recent Items.

Location

```
shell:recent
```

Observed

Shortcut (LNK) files corresponding to recently accessed documents.

---

## Step 5

Reviewed Shortcut Properties.

Observed

- Target file
- Original path
- Last modified timestamp

These artifacts confirmed that the documents had been accessed.

---

## Step 6

Investigated Sysmon Event ID 1.

Observed

Process Creation events for:

```
notepad.exe
```

Verified

- Process Image
- Parent Process (explorer.exe)
- Command Line
- User
- Timestamp

---

## Step 7

Investigated Wazuh.

Threat Hunting Query

```
data.win.system.eventID:1
```

Observed

Successful collection of Notepad process execution events.

---

# Evidence Correlation

Document Created

↓

Document Opened

↓

Explorer launched Notepad

↓

Sysmon Event ID 1 Generated

↓

Wazuh Collected Telemetry

↓

Recent Items Updated (.lnk)

↓

Timeline Reconstruction

---

# DFIR Analysis

The LNK artifacts demonstrated that the documents had been accessed from Windows Explorer.

Sysmon confirmed the execution of Notepad, while Wazuh centralized the endpoint telemetry.

Correlating these sources provided stronger evidence than relying on any single artifact.

---

# MITRE ATT&CK

| Tactic | Technique | ID |
|---------|-----------|----|
| Execution | User Execution | T1204 |
| Collection | Data from Local System | T1005 |

---

# Conclusion

The investigation successfully reconstructed user activity using Windows LNK artifacts, Sysmon Process Creation events, and Wazuh Threat Hunting. This demonstrated how multiple evidence sources can be combined to validate document access during a digital forensic investigation.
