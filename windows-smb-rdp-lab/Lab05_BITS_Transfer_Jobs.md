````md
# Lab05 - Reviewing Windows BITS Transfer Jobs (PowerShell)

## Lab Brief
This lab uses Windows BITS (Background Intelligent Transfer Service) PowerShell cmdlets to review transfer jobs and extract important details that matter in security investigations, such as:
- DisplayName (job name)
- JobState (state of transfer)
- FilesTotal / FilesTransferred (how many files)
- Priority (transfer priority)
- OwnerAccount (who created/owns the job)
- RemoteName (target URL)
- LocalName (where it saves locally)

BITS is often used for legitimate background downloads, but it can also be abused to download payloads quietly, so knowing how to review jobs is important.

---

## What You Successfully Found (From Your Output)

### Windows Security Manager
- FilesTotal: 1
- FilesTransferred: 0
- JobState: Suspended

Evidence (your output):
```powershell
DisplayName      : Windows Security Manager
JobState         : Suspended
FilesTotal       : 1
FilesTransferred : 0
````

Answer for the question:

* How many files are to be transferred (FilesTotal)? 1

---

## Important Note (Why You Got Access Denied)

If you run BITS queries without Administrator privileges, you will get:

* 0x80070005 (E_ACCESSDENIED)

Example errors you got:

```powershell
Get-BitsTransfer : Access is denied. (Exception from HRESULT: 0x80070005 (E_ACCESSDENIED))
bitsadmin ... Unable to enum jobs - 0x80070005 Access is denied.
net session -> System error 5 has occurred. Access is denied.
```

Fix:

* Open PowerShell -> Run as Administrator
* Then run `Get-BitsTransfer -AllUsers`

---

## Commands (Copy/Paste)

### 1) List all BITS jobs (all users)

```powershell
Get-BitsTransfer -AllUsers |
Select-Object DisplayName, JobId, OwnerAccount, JobState, Priority, FilesTotal, FilesTransferred |
Format-Table -Auto
```

### 2) Show only pending/non-transferred jobs

```powershell
Get-BitsTransfer -AllUsers |
Where-Object { $_.JobState -ne "Transferred" } |
Select-Object DisplayName, JobId, OwnerAccount, JobState, Priority, FilesTotal, FilesTransferred |
Format-Table -Auto
```

### 3) Get full details for the job: "Windows Security Manager"

```powershell
Get-BitsTransfer -AllUsers |
Where-Object { $_.DisplayName -eq "Windows Security Manager" -and $_.JobState -ne "Transferred" } |
Select-Object DisplayName, JobState, FilesTotal, FilesTransferred, OwnerAccount, Priority |
Format-List
```

### 4) Get the target URL + local save path for "Windows Security Manager"

This answers: "What is the target URL?"

```powershell
$job = Get-BitsTransfer -AllUsers | Where-Object { $_.DisplayName -eq "Windows Security Manager" }
$job | Get-BitsTransferFile | Select-Object RemoteName, LocalName | Format-List
```

### 5) Windows Administration Tool: identify the downloaded file from the URL

This answers: "Based on the URL, what file is being downloaded?"

```powershell
$job = Get-BitsTransfer -AllUsers | Where-Object { $_.DisplayName -eq "Windows Administration Tool" }
$job | Get-BitsTransferFile | Select-Object RemoteName, LocalName | Format-List
```

Extract only the filename from the RemoteName (URL):

```powershell
$remote = ($job | Get-BitsTransferFile | Select-Object -First 1 -ExpandProperty RemoteName)
($remote -split "/")[-1]
```

### 6) Windows Update Information: priority

This answers: "What priority has it been assigned?"

```powershell
Get-BitsTransfer -AllUsers |
Where-Object { $_.DisplayName -eq "Windows Update Information" } |
Select-Object DisplayName, Priority |
Format-List
```

### 7) Windows Update Information: state

This answers: "What is the state (JobState)?"

```powershell
Get-BitsTransfer -AllUsers |
Where-Object { $_.DisplayName -eq "Windows Update Information" } |
Select-Object DisplayName, JobState |
Format-List
```

Or both together:

```powershell
Get-BitsTransfer -AllUsers |
Where-Object { $_.DisplayName -eq "Windows Update Information" } |
Select-Object DisplayName, Priority, JobState |
Format-List
```

### 8) PuTTY job: owner

This answers: "Who is the owner?"

```powershell
Get-BitsTransfer -AllUsers |
Where-Object { $_.DisplayName -eq "PuTTY: a free SSH and Telnet client" } |
Select-Object DisplayName, OwnerAccount, JobState |
Format-List
```

---

## Lab Results (Fill After You Run Commands)

### Windows Security Manager

* FilesTotal: 1
* JobState: Suspended
* Target URL (RemoteName): ________________________________
* Local Path (LocalName): _________________________________
* OwnerAccount: __________________________________________

### Windows Administration Tool

* Remote URL (RemoteName): ________________________________
* Downloaded file name (from URL): ________________________

### Windows Update Information

* Priority: ______________________________________________
* JobState: ______________________________________________

### PuTTY: a free SSH and Telnet client

* OwnerAccount: __________________________________________
* JobState: ______________________________________________

```
::contentReference[oaicite:0]{index=0}
```
