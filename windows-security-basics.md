# Lab 1: Windows Services – Understanding How They Work

## Purpose
This lab focuses on understanding how Windows services operate, why they exist,
and how their configuration impacts system security.

## What Is a Windows Service?
A Windows service is a background process that:
- Runs without user interaction
- Can start automatically or manually
- Often performs critical system or network functions

## Key Questions When Analyzing a Service
When reviewing any Windows service, always ask:
1. What does this service do?
2. When does it start?
3. Which account does it run under?
4. What privileges does that account have?
5. Is this service necessary on this system?

## Tool Used
- Windows Services Management Console (`services.msc`)

## Example Analysis: DNS Client Service

**Service Name:** DNS Client  
**Service Identifier:** `Dnscache`

### What This Service Does
The DNS Client service resolves domain names to IP addresses and caches results
to improve network performance.

### Execution Context
- Runs under: `NT AUTHORITY\NetworkService`

### Security Notes
- Uses a limited-privilege account
- Follows the principle of least privilege
- Reduces system impact if compromised

## Key Takeaways
- Services often run with elevated privileges
- Misconfigured services increase attack surface
- Least privilege is a core security principle

## Learning Outcome
This lab improves understanding of Windows service behavior and security impact.

## Note
This lab was performed in a controlled environment for educational purposes.
