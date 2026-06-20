# STATIC_ANALYSIS_REPORT_SAMPLE_2.md

## Sample Information

Filename:
dc12faa460faab18a12d8ac33fb3a3a96c95232cff2f124df15300475cc20486.js

Family:
AgentTesla

File Type:
JavaScript

File Size:
3.19 MiB

MD5:
cd66735e5e540b3ec4f0efe41a66e9d0

SHA256:
dc12faa460faab18a12d8ac33fb3a3a96c95232cff2f124df15300475cc20486

## File Identification

Detect It Easy identified the sample as:

- JavaScript
- JavaScript bytecode
- Script-based malware sample

Since the sample is a JavaScript file and not a PE executable, PE header analysis, import tables, and export tables are not applicable.

## String Analysis

Strings extracted:
14,197

### Findings

- Large amount of obfuscated JavaScript content.
- Encoded variable names and functions.
- Repetitive unreadable strings.
- Evidence of string-based obfuscation.

### Interpretation

The sample appears heavily obfuscated to conceal malicious functionality and hinder static analysis.

## Imports and Exports

Not applicable.

Reason:
The sample is a JavaScript file rather than a Windows PE executable.

## Packer / Obfuscation Analysis

Indicators of obfuscation observed:

- High volume of encoded strings.
- Obfuscated variable names.
- Bytecode-like JavaScript structures.
- Concealed functionality through string manipulation.

### Conclusion

The sample appears to be an obfuscated JavaScript-based AgentTesla malware component designed to evade analysis and hide its malicious behavior.