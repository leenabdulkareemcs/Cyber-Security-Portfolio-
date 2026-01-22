# Lab 02 – Windows SMB & RDP
**Cyber Fundamentals | Windows Basics**

---

## Lab Objective
The objective of this lab is to understand how **SMB (Server Message Block)** and **RDP (Remote Desktop Protocol)** are used in Windows environments for **remote access, authentication, and lateral movement**.

This lab demonstrates how credentials discovered through SMB can be leveraged to gain further access using PsExec and RDP.

---

## Key Concepts Covered
- SMB file sharing and authentication  
- Mapping and unmapping network shares  
- Credential switching limitations in Windows  
- PsExec remote command execution  
- RDP authentication and Network Level Authentication (NLA)  
- Credential-based lateral movement  

---

## Lab Environment

| Machine | Role | Notes |
|--------|------|-------|
| Client | Starting machine | Used for SMB, PsExec, and RDP |
| Host 1 | SMB Host | Contains shared files and admin access |
| Host 2 | RDP Host | Target system for RDP access |

---

## 1. Server Message Block (SMB)

SMB is a Windows network protocol that allows:
- File and folder sharing  
- Printer sharing  
- Remote administrative access  
- Interaction with system resources  

SMB operates **without a graphical interface** and is commonly used by both administrators and attackers.

---

## 2. Connecting to SMB Shares

SMB shares can be accessed using Windows Explorer or the command line.

### Managing SMB Sessions

Map a share:
```bash
net use Z: \\<IP>\Share /user:username password
```

Remove all sessions:
```bash
net use * /delete
```

Windows allows only one active SMB session per host.

---

## 3. SMB Versions

| Version | Notes |
|--------|-------|
| SMBv1 | Insecure, guest access |
| SMBv2 | Improved security |
| SMBv3 | Encryption & strongest |

---

## 4. PsExec

PsExec allows remote command execution over SMB.

```bash
PsExec64.exe -i -accepteula \\<IP> -u admin -p <password> cmd
```

Used when:
- RDP is blocked  
- Admin access is available  

---

## 5. Credential Discovery

Credential files discovered via SMB enabled:
- PsExec access  
- Further enumeration  
- Discovery of RDP credentials  

---

## 6. Remote Desktop Protocol (RDP)

- RDP provides full graphical access  
- Requires valid credentials  
- Requires RDP permissions  
- Uses Network Level Authentication (NLA)  

---

## 7. Network Level Authentication (NLA)

NLA:
- Authenticates before session creation  
- Prevents unauthorized access  
- Reduces attack surface  

---

## Lateral Movement Summary

- SMB access exposed credentials  
- PsExec enabled admin command execution  
- RDP credentials discovered  
- RDP access to second host achieved  
- Sensitive files retrieved  

---

## Key Takeaways

- SMB is a powerful attack surface  
- Admin ≠ RDP access  
- Credentials are often stored insecurely  
- Lateral movement is step-by-step  

---

## One-Line Summary

SMB enables file and command access, PsExec enables remote execution, and RDP enables full desktop access — each requiring proper credentials and authentication context.

---

## Revision Notes

- Clear SMB sessions with:
```bash
net use * /delete
```
- PsExec uses SMB, not RDP  
- RDP requires correct user + permissions  
- Always verify which host you are connecting to
