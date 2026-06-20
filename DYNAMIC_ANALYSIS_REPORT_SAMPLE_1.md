# DYNAMIC_ANALYSIS_REPORT_SAMPLE_1.md

# Dynamic Analysis Report – Sample 1 (AsyncRAT)

## Sample Information

**Malware Family:** AsyncRAT

**Filename:** ac83c85c10b1586723818f43b9dcafcefd46d8d6000984fe489bb1d219ea8b4f9.exe

**File Type:** PE32 Executable

**SHA256:** ac83c85c10b1586723818f43b9dcafcefd46d8d6000984fe489bb1d219ea8b4f9

**MD5:** 95ca5b8c1bfcd91a4b4a48d22baf16e2

---

# Analysis Environment

## Host System

* HP ProBook 440 G8
* Intel Core i5-1135G7
* 16 GB RAM
* Windows 11

## Virtual Environment

* Oracle VirtualBox
* Windows 10 (64-bit)
* 4096 MB RAM
* 3 CPUs
* 40 GB Dynamic Disk

## Security Configuration

* Shared Clipboard Disabled
* Drag & Drop Disabled
* Shared Folders Disabled

## Network Configuration

* Host-Only Adapter
* IPv4 Address: 192.168.56.101
* No Internet Connectivity

Verification:

```text
ping 8.8.8.8

Result:
PING transmit failed. General failure.
100% packet loss
```

---

# Tools Used

* Process Monitor (Procmon)
* Process Hacker
* RegShot
* Wireshark

---

# Baseline Snapshot

A baseline registry snapshot was captured using RegShot before malware execution.

Snapshot Details:

* Registry Keys Scanned: 383,049
* Registry Values Scanned: 652,763

This baseline was used for comparison after execution.

---

# Malware Execution

The sample was executed inside the isolated Windows 10 virtual machine.

Execution Method:

```text
Run as Administrator
```

Monitoring tools remained active during execution.

Observation Period:

```text
Approximately 5 minutes
```

---

# Process Activity Analysis

Process Hacker was used to monitor process creation and system activity.

## Observations

No significant child processes were observed.

The following commonly abused processes were not spawned:

* cmd.exe
* powershell.exe
* wscript.exe
* cscript.exe
* rundll32.exe

## Service Creation

A service creation event was detected during execution.

Service Name:

```text
ncoysosj
```

Verification:

```cmd
sc query ncoysosj
```

Output:

```text
TYPE: KERNEL_DRIVER
STATE: STOPPED
WIN32_EXIT_CODE: 1077 (0x435)
```

### Interpretation

The malware attempted to create a kernel-driver service.

The service was not actively running at the time of verification.

This behavior suggests an attempt to establish persistence or deploy a driver component.

---

# File System Activity Analysis

Process Monitor recorded multiple filesystem operations.

Observed Operations:

* CreateFile
* CreateFileMapping
* QueryBasicInformationFile
* CloseFile

### Interpretation

The malware actively interacted with the filesystem during execution.

These operations indicate normal execution activity and possible preparation for persistence or payload deployment.

---

# Registry Activity Analysis

RegShot comparison was performed after execution.

## Comparison Results

* Keys Deleted: 6
* Values Deleted: 6
* Values Modified: 37

Total Changes:

```text
49
```

### Observations

Most detected registry changes were associated with normal user activity and analysis tools including:

* RegShot
* Process Hacker
* Wireshark
* Windows Explorer

No conclusive malware persistence registry entries were identified during the observation period.

---

# Network Activity Analysis

Wireshark was used to monitor network communications.

## Observations

No network packets were captured during execution.

Observed Traffic:

```text
No DNS Requests
No HTTP Traffic
No HTTPS Traffic
No TCP Connections
```

### Interpretation

The sample was executed within a Host-Only isolated environment.

The absence of external connectivity prevented communication with potential command-and-control infrastructure.

---

# Behavioral Summary

The following behaviors were observed:

* Successful execution inside isolated VM
* Multiple filesystem interactions
* Creation of kernel-driver service "ncoysosj"
* No visible child process creation
* No successful network communications
* Limited registry modifications observed

---

# Indicators of Compromise (IOCs)

## File Indicators

| Type     | Value                                                                 |
| -------- | --------------------------------------------------------------------- |
| Filename | ac83c85c10b1586723818f43b9dcafcefd46d8d6000984fe489bb1d219ea8b4f9.exe |
| MD5      | 95ca5b8c1bfcd91a4b4a48d22baf16e2                                      |
| SHA256   | ac83c85c10b1586723818f43b9dcafcefd46d8d6000984fe489bb1d219ea8b4f9     |

## Service Indicators

| Type         | Value         |
| ------------ | ------------- |
| Service Name | ncoysosj      |
| Service Type | Kernel Driver |
| State        | Stopped       |

---

# Conclusion

Dynamic analysis confirmed that the AsyncRAT sample executed successfully inside the isolated Windows 10 malware analysis environment.

The malware performed filesystem operations and created a kernel-driver service named "ncoysosj", indicating a possible persistence or driver installation attempt. No successful network communications were observed due to the Host-Only network configuration. Registry analysis identified minor system changes but no conclusive persistence-related registry modifications.

Overall, the sample exhibited behavior consistent with malicious software and demonstrated an attempt to modify the system through service creation.
