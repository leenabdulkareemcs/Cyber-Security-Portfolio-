# Lab05 — Windows BITS Jobs Review (PowerShell)

## Purpose
This lab focuses on reviewing Windows Background Intelligent Transfer Service (BITS) jobs to identify pending transfers and extract key job details such as:
- DisplayName
- JobState
- FilesTotal / FilesTransferred
- OwnerAccount
- Priority
- Target URL (RemoteName) and Local path (LocalName)

BITS runs background downloads for Windows and applications. Reviewing BITS jobs is useful for troubleshooting and basic security monitoring.

---

## Requirement (Permissions)
To view jobs for **all users**, you must run PowerShell **as Administrator**.
If you see: `Access is denied (0x80070005)`, it usually means you are not elevated.

How to run PowerShell as Administrator:
- Start Menu -> PowerShell -> Right click -> Run as administrator

---

## Part 1 — Your Attempts (Commands + Outputs)

### 1) List all BITS jobs for all users (failed)
Command:
```powershell
powershell -NoProfile -Command "Get-BitsTransfer -AllUsers | Select-Object DisplayName,JobId,OwnerAccount,JobState,CreationTime | Format-Table -Auto"
````

Output:

```text
Get-BitsTransfer : Access is denied. (Exception from HRESULT: 0x80070005 (E_ACCESSDENIED))
At line:1 char:1
+ Get-BitsTransfer -AllUsers | Select-Object DisplayName,JobId,OwnerAcc ...
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : PermissionDenied: (:) [Get-BitsTransfer], UnauthorizedAccessException
    + FullyQualifiedErrorId : GetBitsTransferAuthException,Microsoft.BackgroundIntelligentTransfer.Management.GetBitsTransfer

Get-BitsTransfer : Access is denied. (Exception from HRESULT: 0x80070005 (E_ACCESSDENIED))
At line:1 char:1
+ Get-BitsTransfer -AllUsers | Select-Object DisplayName,JobId,OwnerAcc ...
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (:) [Get-BitsTransfer], UnauthorizedAccessException
    + FullyQualifiedErrorId : System.UnauthorizedAccessException,Microsoft.BackgroundIntelligentTransfer.Management.GetBitsTransfer
```

### 2) List only non-transferred jobs (failed)

Command:

```powershell
powershell -NoProfile -Command "Get-BitsTransfer -AllUsers | Where-Object { $_.JobState -ne 'Transferred' } | Select DisplayName,JobId,OwnerAccount,JobState | ft -Auto"
```

Output:

```text
Get-BitsTransfer : Access is denied. (Exception from HRESULT: 0x80070005 (E_ACCESSDENIED))
At line:1 char:1
+ Get-BitsTransfer -AllUsers | Where-Object { .JobState -ne 'Transferre ...
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : PermissionDenied: (:) [Get-BitsTransfer], UnauthorizedAccessException
    + FullyQualifiedErrorId : GetBitsTransferAuthException,Microsoft.BackgroundIntelligentTransfer.Management.GetBitsTransfer

Get-BitsTransfer : Access is denied. (Exception from HRESULT: 0x80070005 (E_ACCESSDENIED))
At line:1 char:1
+ Get-BitsTransfer -AllUsers | Where-Object { .JobState -ne 'Transferre ...
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (:) [Get-BitsTransfer], UnauthorizedAccessException
    + FullyQualifiedErrorId : System.UnauthorizedAccessException,Microsoft.BackgroundIntelligentTransfer.Management.GetBitsTransfer
```

### 3) Query job: "Windows Security Manager" with file counters (failed)

Command:

```powershell
Get-BitsTransfer -AllUsers |
Where-Object { $_.DisplayName -eq "Windows Security Manager" } |
Select-Object DisplayName, JobId, OwnerAccount, JobState, FilesTotal, FilesTransferred |
Format-List
```

Output:

```text
Get-BitsTransfer : Access is denied. (Exception from HRESULT: 0x80070005 (E_ACCESSDENIED))
At line:1 char:1
+ Get-BitsTransfer -AllUsers |
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : PermissionDenied: (:) [Get-BitsTransfer], UnauthorizedAccessException
    + FullyQualifiedErrorId : GetBitsTransferAuthException,Microsoft.BackgroundIntelligentTransfer.Management.GetBitsTransfer

Get-BitsTransfer : Access is denied. (Exception from HRESULT: 0x80070005 (E_ACCESSDENIED))
At line:1 char:1
+ Get-BitsTransfer -AllUsers |
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (:) [Get-BitsTransfer], UnauthorizedAccessException
    + FullyQualifiedErrorId : System.UnauthorizedAccessException,Microsoft.BackgroundIntelligentTransfer.Management.GetBitsTransfer
```

### 4) bitsadmin list all users verbose (failed)

Command:

```cmd
C:\Users>bitsadmin /list /allusers /verbose
```

Output:

```text
BITSADMIN version 3.0
BITS administration utility.
(C) Copyright Microsoft Corp.

Unable to enum jobs - 0x80070005
Access is denied.
```

Command:

```cmd
C:\Users>bitsadmin /list /allusers /verbose | more
```

Output:

```text
BITSADMIN version 3.0
BITS administration utility.
(C) Copyright Microsoft Corp.

Unable to enum jobs - 0x80070005
Access is denied.
```

### 5) Create a task to run bitsadmin as SYSTEM (failed)

Command:

```cmd
C:\Users>schtasks /create /tn TempBITS /sc once /st 00:00 /ru SYSTEM /tr "cmd /c bitsadmin /list /allusers /verbose > C:\Windows\Temp\bits.txt" /f
```

Output:

```text
WARNING: Task may not run because /ST is earlier than current time.
ERROR: Access is denied.
```

Command:

```cmd
C:\Users>schtasks /run /tn TempBITS
```

Output:

```text
ERROR: The system cannot find the file specified.
```

Command:

```cmd
C:\Users>timeout /t 3 >nul
```

Output:

```text
```

### 6) net session check (failed first)

Command:

```cmd
C:\Users>net session
```

Output:

```text
System error 5 has occurred.

Access is denied.
```

---

## Part 2 — Running PowerShell Elevated (Successful)

### 1) net session (success)

Command:

```powershell
PS C:\WINDOWS\system32> net session
```

Output:

```text
There are no entries in the list.
```

### 2) Find the pending transfer: "Windows Security Manager" (success)

Command:

```powershell
Get-BitsTransfer -AllUsers |
Where-Object { $_.DisplayName -eq "Windows Security Manager" -and $_.JobState -ne "Transferred" } |
Select-Object DisplayName, JobState, FilesTotal, FilesTransferred |
Format-List
```

Output:

```text
DisplayName      : Windows Security Manager
JobState         : Suspended
FilesTotal       : 1
FilesTransferred : 0
```

Lab Answer:

```text
FilesTotal = 1
```

---

## Part 3 — Commands to Answer the Remaining Lab Questions (Copy/Paste Ready)

### Q1) How many files are to be transferred as part of the BITS job named "Windows Security Manager"?

Command:

```powershell
Get-BitsTransfer -AllUsers |
Where-Object { $_.DisplayName -eq "Windows Security Manager" -and $_.JobState -ne "Transferred" } |
Select-Object DisplayName, JobState, FilesTotal, FilesTransferred |
Format-List
```

Expected field to read:

```text
FilesTotal
```

### Q2) What is the target URL of the BITS job named "Windows Security Manager"?

Command:

```powershell
Get-BitsTransfer -AllUsers |
Where-Object { $_.DisplayName -eq "Windows Security Manager" } |
Get-BitsTransferFile |
Select-Object RemoteName, LocalName |
Format-List
```

Where to read:

* `RemoteName` = target URL
* `LocalName` = file path on disk

### Q3) Based on the URL of the job named "Windows Administration Tool", what file is being downloaded?

Command (show full URL + local path):

```powershell
Get-BitsTransfer -AllUsers |
Where-Object { $_.DisplayName -eq "Windows Administration Tool" } |
Get-BitsTransferFile |
Select-Object RemoteName, LocalName |
Format-List
```

Command (extract only the file name from URL):

```powershell
$remote = (Get-BitsTransfer -AllUsers |
Where-Object { $_.DisplayName -eq "Windows Administration Tool" } |
Get-BitsTransferFile |
Select-Object -First 1 -ExpandProperty RemoteName)

($remote -split "/")[-1]
```

### Q4) What priority has the job named "Windows Update Information" been assigned?

Command:

```powershell
Get-BitsTransfer -AllUsers |
Where-Object { $_.DisplayName -eq "Windows Update Information" } |
Select-Object DisplayName, Priority |
Format-List
```

### Q5) What is the state of the "Windows Update Information" BITS transfer job?

Command:

```powershell
Get-BitsTransfer -AllUsers |
Where-Object { $_.DisplayName -eq "Windows Update Information" } |
Select-Object DisplayName, JobState |
Format-List
```

### Q6) Who is the owner of the job named "PuTTY: a free SSH and Telnet client"?

Command:

```powershell
Get-BitsTransfer -AllUsers |
Where-Object { $_.DisplayName -eq "PuTTY: a free SSH and Telnet client" } |
Select-Object DisplayName, OwnerAccount |
Format-List
```

---

## Notes

* `Get-BitsTransfer -AllUsers` needs Administrator.
* To inspect the actual URL/file being transferred, use `Get-BitsTransferFile`.
* Common job states include: Suspended, Transferring, Queued, Transferred, Error.
* In your confirmed output:

  * "Windows Security Manager" is `Suspended`
  * It has `FilesTotal: 1`
  * It has `FilesTransferred: 0`

```
::contentReference[oaicite:0]{index=0}
```
