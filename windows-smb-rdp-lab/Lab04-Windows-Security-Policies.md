# Lab 04 – Windows Security Policies
Cyber Fundamentals | Windows Basics

-----------------------------------------------------------------------

PURPOSE
This lab focuses on understanding Windows Security Policies and how they
are managed using Local Security Policy and Group Policy. It documents
how to access and enumerate security-related settings using the Microsoft
Management Console (MMC).

-----------------------------------------------------------------------

WINDOWS SECURITY POLICIES
Windows Security Policies are configuration rules that control how the
operating system enforces security. These policies help protect systems
against unauthorized access and misuse.

Security policies govern:
- Password complexity and length
- Account lockout behavior
- User rights and privileges
- Auditing and logging behavior
- Access control to system resources

-----------------------------------------------------------------------

GROUP POLICY
Group Policy is a centralized management mechanism used in Active
Directory environments. It allows administrators to configure and enforce
security settings across multiple systems.

Key functions of Group Policy:
- Enforce password and lockout policies
- Apply consistent security settings across users and computers
- Control user environments and application behavior
- Reduce configuration errors through automation

Group Policy is typically used in:
- Domain-joined systems
- Enterprise or organizational networks

-----------------------------------------------------------------------

LOCAL SECURITY POLICY
Local Security Policy is a standalone version of Group Policy used on
non-domain or individual systems. It allows administrators to configure
security settings for a single machine.

Capabilities include:
- Configuring password and account policies
- Assigning user rights (log on locally, shut down system)
- Defining audit policies
- Applying local security best practices

Local Security Policy is managed through the Microsoft Management Console.

-----------------------------------------------------------------------

MICROSOFT MANAGEMENT CONSOLE (MMC)
The Microsoft Management Console (mmc.exe) is a framework that hosts
administrative tools known as snap-ins. It provides a centralized
interface for system management.

Relevant security-related snap-ins:
- Group Policy Object Editor
- Local Security Policy

MMC allows administrators to:
- View security configurations
- Modify policy settings
- Save custom management consoles

-----------------------------------------------------------------------

ACCESSING SECURITY POLICIES USING MMC

Steps:
1. Press Windows + R
2. Type: mmc.exe
3. Press Enter
4. From the File menu, select Add/Remove Snap-in
5. Select Group Policy Object Editor or Local Security Policy
6. Click Add
7. Choose Local Computer when prompted
8. Click Finish, then OK

Once loaded, navigate through the policy tree to view settings.

-----------------------------------------------------------------------

KEY SECURITY POLICY CATEGORIES

Common areas examined in this lab include:
- Account Policies
  - Password Policy
  - Account Lockout Policy
- Local Policies
  - Audit Policy
  - User Rights Assignment
  - Security Options

These settings directly affect system security posture.

-----------------------------------------------------------------------

IN THIS LAB (PRACTICAL TASK)

Objective:
Use the Microsoft Management Console to view and enumerate Windows
security policies on the local system.

Tasks performed:
- Open MMC
- Add the appropriate security policy snap-in
- Navigate through policy categories
- Identify and review configured security settings

No policy modifications were required.

-----------------------------------------------------------------------

SECURITY NOTES
Security policies are a critical defense mechanism in Windows systems.
Misconfigured policies can result in:
- Weak authentication controls
- Excessive user privileges
- Insufficient auditing and monitoring

Regular review of security policies is essential for maintaining system
integrity and compliance.

-----------------------------------------------------------------------

KEY TAKEAWAYS
- Windows Security Policies control system-level security behavior
- Group Policy is used for centralized management
- Local Security Policy is used for standalone systems
- MMC provides a unified interface for policy management
- Proper policy configuration is essential for system security

-----------------------------------------------------------------------

REVISION NOTES
- Know the difference between Group Policy and Local Security Policy
- Understand how to access policies using MMC
- Be familiar with common policy categories
- Always review security settings before making changes
