# STATIC_ANALYSIS_REPORT_SAMPLE_1

## Sample Information

Malware Family: AsyncRAT

Filename:
ac83c85c10b1586723818f43b9dcafcefd46d8d6000984fe489bb1d219ea8b4f9.exe

File Type:
PE32 Executable

File Size:
713.00 KiB

MD5:
95ca5b8c1bfcd91a4b4a48d22baf16e2

SHA256:
ac83c85c10b1586723818f43b9dcafcefd46d8d6000984fe489bb1d219ea8b4f9

---

## File Identification

Tool Used:
Detect It Easy (DIE)

Format:
PE32

Architecture:
I386

Mode:
32-bit

Type:
GUI

Compiler:
VB.NET

Language:
VB.NET

Linker:
Microsoft Linker

Framework:
.NET Framework 4.5 (CLR 4.0.30319)

Observation:
The sample is a 32-bit Windows executable developed using VB.NET and targets the Microsoft .NET Framework.

---

## PE Header Analysis

Base Address:
0x00400000

Entry Point:
0x004AE1FA

Image Size:
0x000B8000

Number of Sections:
3

Observation:
The executable uses a valid PE32 structure and runs through the .NET Common Language Runtime (CLR).

---

## Imports and Exports Analysis

Imported DLL:

- mscoree.dll

Imported Function:

- _CorExeMain

Exports:

- None detected

Observation:
The malware executes through the .NET runtime using mscoree.dll. The _CorExeMain function confirms that it is a managed .NET application.

---

## String Analysis

Tool Used:
Detect It Easy (DIE)

Notable String Found:

- Microsoft.VisualBasic

Findings:

- VB.NET runtime references identified.
- .NET related strings present.
- No clear URLs detected.
- No Pastebin references found.
- No AppData references found.

Observation:
The presence of Microsoft.VisualBasic confirms the use of VB.NET. The absence of obvious indicators suggests possible string obfuscation or runtime string generation.

---

## Packer / Obfuscation Detection

Tool Used:
Detect It Easy (DIE)

Overall Entropy:
7.89883

Detection Result:
Packed (98%)

Section Analysis:

.rsrc
Entropy: 7.83622
Status: Packed

.reloc
Entropy: 0.10191
Status: Not Packed

Observation:
The high entropy value indicates compression, encryption, or packing. The .rsrc section appears heavily packed and may contain encrypted or compressed resources.

---

## Conclusion

The sample is a 32-bit VB.NET based AsyncRAT executable targeting the .NET Framework 4.5 environment.

Static analysis identified:

- PE32 executable structure
- VB.NET compiler
- .NET runtime dependency
- Managed code execution through CLR
- High entropy value
- Packed/obfuscated resources

The characteristics observed are consistent with known AsyncRAT malware samples used for remote access and system compromise.

---

## Tools Used

- Detect It Easy (DIE)
- CFF Explorer
- CertUtil
- Strings Analysis