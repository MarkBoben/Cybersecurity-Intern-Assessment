# LAB_SETUP.md

## Overview

This document describes the isolated lab environment used to perform static and dynamic malware analysis as part of the Cybersecurity Intern Assessment. All analysis was conducted in a controlled, network-isolated virtual environment to prevent any risk to production systems or external networks.

---

## Table of Contents

- [Host Environment](#host-environment)
- [Virtual Machine Configuration](#virtual-machine-configuration)
- [Network Isolation](#network-isolation)
- [VM Hardening / Anti-Leak Settings](#vm-hardening--anti-leak-settings)
- [Analysis Tools Installed](#analysis-tools-installed)
- [Snapshot Strategy](#snapshot-strategy)
- [Verification Steps](#verification-steps)

---

## Host Environment

- **Hypervisor:** Oracle VirtualBox
- **Host OS:** Kali Linux (used for Wireshark traffic capture and Ghidra reverse engineering)
- **Detonation VM:** Windows 10 (64-bit) — used to safely execute and observe malware samples

Two virtual machines were maintained side by side in VirtualBox Manager: a Kali Linux VM for analysis tooling, and a dedicated Windows 10 VM (`MalwareLab-Win10`) used purely for malware detonation.

![VirtualBox Manager Overview](Windows_VM_installed.png)

---

## Virtual Machine Configuration

| Setting | Value |
|---|---|
| VM Name | MalwareLab-Win10 |
| Guest OS | Windows 10 (64-bit) |
| Base Memory | 4096 MB |
| Processors | 3 |
| Video Memory | 256 MB |
| Graphics Controller | VBoxSVGA |
| Storage Controller | SATA |
| Disk | MalwareLab-Win10.vdi (Normal, 40.00 GB) |
| Acceleration | Nested Paging, Hyper-V Paravirtualization |

A clean installation of Windows 10 was completed and verified booting correctly before any tools or samples were introduced.

![Clean Windows Install](Clean_Windows_Install.png)

---

## Network Isolation

The Windows analysis VM's network adapter was configured to use a **Host-Only Adapter** rather than NAT or Bridged networking. This ensures the VM has no route to the public internet while still allowing local capture of any traffic the malware attempts to generate.

| Setting | Value |
|---|---|
| Adapter | Adapter 1 |
| Attached To | Host-only Adapter |
| Adapter Name | VirtualBox Host-Only Ethernet Adapter |
| Adapter Type | Intel PRO/1000 MT Desktop (82540EM) |
| Promiscuous Mode | Deny |

![Network Isolated - Host Only](Network_isolated-Host-Only.png)

Isolation was verified from inside the guest using `ipconfig`, confirming the VM received a host-only IP with no default gateway configured (i.e., no path to the internet):

```
IPv4 Address. . . . . . . . . . . : 192.168.56.101
Subnet Mask . . . . . . . . . . . : 255.255.255.0
Default Gateway . . . . . . . . . :
```

![Ipconfig Verification](Ipconfig_verification_completed.png)

The absence of a Default Gateway confirms the VM cannot route traffic externally, satisfying the network isolation requirement.

---

## VM Hardening / Anti-Leak Settings

To reduce the risk of accidental data transfer between host and guest, the following VirtualBox features were explicitly disabled:

| Feature | Status |
|---|---|
| Shared Clipboard | Disabled |
| Drag-and-Drop | Disabled |

![Shared Clipboard Disabled](Shared_Clipboard_disabled.png)
![Drag and Drop Disabled](Drag___Drop_disabled.png)

No shared folders were configured between host and guest, further reducing the risk of malware escaping the sandboxed environment.

---

## Analysis Tools Installed

The following free tools were installed inside the Windows analysis VM prior to introducing any malware samples:

| Tool | Purpose |
|---|---|
| Detect It Easy (DIE) | File identification, packer/obfuscation detection, entropy analysis |
| PEStudio | Static PE analysis |
| Explorer Suite (CFF Explorer) | PE header inspection |
| HashMyFiles | File hashing |
| Process Monitor (Procmon) | Real-time file system / registry / process activity monitoring |
| Strings | String extraction |
| Process Hacker | Live process, service, and network inspection |
| RegShot | Registry/filesystem baseline comparison (before/after snapshots) |
| Wireshark | Network traffic capture (run from the Kali host, observing the host-only network segment) |

![Analysis Tools Folder](Analysis_tools.png)

---

## Snapshot Strategy

Snapshots were taken at key checkpoints to allow reverting the VM to a known-clean state before and after each sample detonation:

1. **Clean Install** — taken immediately after Windows installation, before any tools were added.
2. **Tools Installed** — taken after all analysis tools were installed and verified working, before any sample was introduced.

This snapshot strategy ensures each malware sample is analyzed against an identical, uncontaminated baseline, and allows the environment to be reset between samples to avoid cross-contamination of results.

---

## Verification Steps

Before proceeding to sample acquisition and analysis, the following was confirmed:

- [x] Windows 10 VM boots cleanly
- [x] Network adapter set to Host-Only (no internet access)
- [x] `ipconfig` confirms no default gateway / no external route
- [x] Shared Clipboard disabled
- [x] Drag-and-Drop disabled
- [x] No shared folders configured
- [x] All required analysis tools installed and accessible
- [x] Baseline snapshot taken prior to any sample execution

With the lab environment isolated, hardened, and verified, the environment was considered ready for malware sample acquisition and analysis (see `STATIC_ANALYSIS_REPORT.md` and `DYNAMIC_ANALYSIS_REPORT.md`).
