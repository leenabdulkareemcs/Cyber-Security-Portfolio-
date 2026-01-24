# Lab06 — Windows Concepts: CertUtil (Practical Lab)

## Purpose
This lab introduces **CertUtil**, a built-in Windows utility used for certificate operations and file handling. You will practice:
- Understanding what CertUtil is and why it matters
- Encoding a file to Base64 (`-encode`)
- Decoding a Base64 file back to the original (`-decode`)
- Identifying file types using **magic bytes** and Base64 headers
- Learning how attackers abuse CertUtil for stealthy downloads and decoding

---

## Background (Quick Brief)

### CertUtil
`certutil.exe` is a Windows utility commonly used to manage certificates and view CA configuration. It also supports useful file features like:
- Hashing (checksums)
- Encoding/decoding (Base64 / Hex)
- Downloading files from the internet (in some usage)

Because it is a trusted Windows tool, it is sometimes abused by malware.

### Certificates and CAs
A **Certificate Authority (CA)** is a trusted entity that issues **digital certificates**. Certificates help verify identity and enable secure communication (TLS/HTTPS).

### Encoding and Magic Bytes
Many certificate files are Base64 encoded.
Most file types have identifying bytes at the beginning called **magic bytes** (file signature).

Example:
- `.exe` magic bytes often start with: `MZ` (hex: `4D 5A`)
- If a PE/EXE is Base64 encoded, the first Base64 characters can help identify it too (example: `TVqQAA...`)

---

## Why CertUtil is Abused
Attackers may:
- Download payloads disguised as certificates or Base64 files
- Decode them locally into executable binaries
- Bypass controls because CertUtil is a legitimate Windows utility

Common abuse idea:
1) download encoded payload  
2) decode into executable  
3) run it  

---

## Lab Tasks (Commands + Outputs)

## Part 1 — Check CertUtil Help and Location

Command:
```powershell
where certutil
````

Command:

```powershell
certutil -?
```

Expected Output (example):

```text
C:\Windows\System32\certutil.exe
```

---

## Part 2 — Create a Test File (Payload Example)

Command:

```powershell
echo This is a test file for Lab06 > sample.txt
type sample.txt
```

Expected Output:

```text
This is a test file for Lab06
```

---

## Part 3 — Encode the File to Base64

Command:

```powershell
certutil -encode sample.txt sample_encoded.txt
```

Expected Output (example):

```text
Input Length = ...
Output Length = ...
CertUtil: -encode command completed successfully.
```

Open the Base64 file:

```powershell
notepad sample_encoded.txt
```

What you should see (example format):

```text
-----BEGIN CERTIFICATE-----
VGhpcyBpcyBhIHRlc3QgZmlsZSBmb3IgTGFiMDYK
-----END CERTIFICATE-----
```

Note:

* CertUtil wraps the Base64 inside BEGIN/END lines (looks like a certificate block)

---

## Part 4 — Decode Back to Original

Command:

```powershell
certutil -decode sample_encoded.txt sample_decoded.txt
```

Expected Output (example):

```text
Input Length = ...
Output Length = ...
CertUtil: -decode command completed successfully.
```

Verify:

```powershell
type sample_decoded.txt
```

Expected Output:

```text
This is a test file for Lab06
```

---

## Part 5 — Check File Hash (Integrity Check)

Command:

```powershell
certutil -hashfile sample.txt SHA256
certutil -hashfile sample_decoded.txt SHA256
```

Expected Result:

* The SHA256 hash for both files should match (meaning decode restored the exact content)

Expected Output (example):

```text
SHA256 hash of sample.txt:
<hash value>
CertUtil: -hashfile command completed successfully.
```

---

## Part 6 — Magic Bytes Concept (Demo)

If you have an EXE file (example: `C:\Windows\System32\notepad.exe`), you can inspect the first bytes.

PowerShell command:

```powershell
$bytes = Get-Content C:\Windows\System32\notepad.exe -Encoding Byte -TotalCount 2
$bytes
```

Expected Output (example):

```text
77
90
```

77 and 90 in ASCII = `MZ` (typical EXE signature)

---

## Security Notes (Defender Perspective)

CertUtil usage becomes suspicious when you see patterns like:

* Downloading from unusual domains
* Encoding/decoding then executing right after
* Writing files into temp directories
* Renaming certutil.exe or copying it to new names

---

## Summary Answers (What you learned)

* CertUtil is a legitimate Windows tool for certificate and file operations
* Base64 encoding can hide the real nature of a file
* Magic bytes help identify file types, even if renamed
* Malware can abuse CertUtil to download + decode payloads in a stealthy way

---

## Command Syntax Reference

```text
certutil.exe [Options] [InFile] [OutFile]
```

Common options used in this lab:

```powershell
certutil -encode <InFile> <OutFile>
certutil -decode <InFile> <OutFile>
certutil -hashfile <File> <Algorithm>
```

```
::contentReference[oaicite:0]{index=0}
```
