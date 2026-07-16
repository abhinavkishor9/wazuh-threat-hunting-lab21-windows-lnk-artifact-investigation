# Troubleshooting Notes

## Issue 1

### No LNK files found in Recent Items

Cause

Windows may not immediately create Recent Item shortcuts depending on application behavior or system configuration.

Resolution

- Open the document directly from Windows Explorer.
- Leave the document open for a few seconds before closing it.
- Check the Recent Items folder again using:

```
shell:recent
```

---

## Issue 2

### Recent Items folder appears empty

Cause

The Recent Items feature may be disabled or no recent documents have been recorded.

Resolution

- Open multiple documents normally from File Explorer.
- Refresh the Recent Items folder.
- Verify that shortcut files are created.

---

## Issue 3

### No Sysmon Event ID 1

Cause

Sysmon Process Creation monitoring is disabled or the event has not yet been generated.

Resolution

Verify Sysmon service:

```powershell
Get-Service Sysmon64
```

Open the document again and review the Sysmon Operational log.

---

## Issue 4

### No results in Wazuh

Cause

The dashboard time range is incorrect or events have not yet been indexed.

Resolution

- Set the time range to **Last 15 Minutes** or **Last 1 Hour**.
- Refresh the Threat Hunting page.
- Search:

```
data.win.system.eventID:1
```

---

## Issue 5

### Unable to find Notepad events

Cause

Multiple Process Creation events may exist.

Resolution

Search specifically for:

```
notepad.exe
```

Review the process image and command line to locate the correct event.

---

## Issue 6

### Shortcut properties do not match expectations

Cause

The shortcut may reference a different recently opened file.

Resolution

Verify the shortcut filename and open the correct **Properties** window to confirm the target path.

---

# Lessons Learned

- Windows LNK artifacts provide valuable evidence of user activity.
- Sysmon Event ID 1 confirms application execution.
- Wazuh centralizes endpoint telemetry for investigation.
- Correlating forensic artifacts with endpoint logs produces stronger investigative findings than relying on a single evidence source.

---

# Final Status

✅ Monitoring verified

✅ Investigation documents created

✅ User activity simulated

✅ LNK artifacts identified

✅ Sysmon Process Creation events confirmed

✅ Wazuh investigation completed

✅ User activity timeline reconstructed

The lab successfully demonstrated how Windows Shortcut (LNK) artifacts can be combined with Sysmon and Wazuh to investigate document access and reconstruct user activity during a DFIR investigation.
