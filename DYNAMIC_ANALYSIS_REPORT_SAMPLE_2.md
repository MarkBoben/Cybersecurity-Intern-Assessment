# DYNAMIC_ANALYSIS_REPORT_SAMPLE_2.md

# Dynamic Analysis Report – Sample 2 (AgentTesla JavaScript)

## Sample Information

**Malware Family:** AgentTesla

**Filename:** dc12faa460faab18a12d8ac33fb3a3a96c95232cff2f124df15300475cc20486.js

**File Type:** JavaScript

**SHA256:** dc12faa460faab18a12d8ac33fb3a3a96c95232cff2f124df15300475cc20486

**MD5:** cd66735e5e540b3ec4f0efe41a66e9d0

---

# Analysis Environment

## Virtual Machine

* Windows 10 (64-bit)
* Oracle VirtualBox
* Host-Only Network

## Monitoring Tools

* Process Monitor (Procmon)
* Process Hacker
* RegShot
* Wireshark

---

# Baseline Snapshot

A baseline registry snapshot was captured using RegShot before execution.

The baseline was used for comparison after malware execution.

---

# Malware Execution

The JavaScript sample was executed inside the isolated malware analysis environment.

Execution was monitored using Procmon, Process Hacker, Wireshark, and RegShot.

Observation period:

* Approximately 5 minutes

---

# Process Activity Analysis

Process Hacker was used to monitor process creation and execution behavior.

## Observations

No suspicious child processes were observed during execution.

The following commonly abused processes were not observed:

* wscript.exe
* cscript.exe
* powershell.exe
* cmd.exe
* mshta.exe

No evidence of process injection was identified.

---

# File System Activity Analysis

Process Monitor recorded filesystem interactions during execution.

Observed operations included:

* LockFile
* UnlockFileSingle
* RegQueryKey
* RegOpenKey
* RegQueryValue

The activity appeared to be primarily associated with Windows system processes and Explorer activity.

No dropped executable payloads were conclusively identified during the observation period.

---

# Registry Activity Analysis

RegShot comparison identified substantial registry modifications.

## Results

Total Changes:

44476

### Common Areas Modified

* HKLM\DRIVERS\DriverDatabase
* Windows Shell Bags
* UserAssist Entries
* AppModel Entries

### Interpretation

A large number of registry modifications were observed. Most changes appeared related to normal Windows activity, shell interactions, and application execution tracking.

No definitive persistence-related registry keys were conclusively identified during the monitoring period.

---

# Network Activity Analysis

Wireshark was used to monitor network communications.

## Observations

No successful network communications were observed.

The malware was executed within a Host-Only isolated environment without internet access.

No DNS requests, HTTP traffic, HTTPS traffic, or outbound TCP connections were identified.

---

# Behavioral Summary

Observed behaviors include:

* Successful script execution
* Extensive registry modifications
* System and Explorer registry activity
* No visible process spawning
* No observable process injection
* No successful network communications

---

# Indicators of Compromise (IOCs)

## File Indicators

| Type     | Value                                                               |
| -------- | ------------------------------------------------------------------- |
| Filename | dc12faa460faab18a12d8ac33fb3a3a96c95232cff2f124df15300475cc20486.js |
| MD5      | cd66735e5e540b3ec4f0efe41a66e9d0                                    |
| SHA256   | dc12faa460faab18a12d8ac33fb3a3a96c95232cff2f124df15300475cc20486    |

---

# Conclusion

Dynamic analysis of the AgentTesla JavaScript sample revealed extensive registry modifications and normal Windows process activity. No malicious child processes, process injection activity, or successful network communications were observed during execution. The Host-Only network configuration prevented external communications and limited behavioral visibility. The sample exhibited behavior consistent with an obfuscated script-based malware component, although no definitive persistence mechanisms were observed during the monitoring period.
