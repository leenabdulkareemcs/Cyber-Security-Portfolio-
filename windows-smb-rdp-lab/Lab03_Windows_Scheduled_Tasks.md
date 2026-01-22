# Lab 03 – Windows Scheduled Tasks
Cyber Fundamentals | Windows Basics

-----------------------------------------------------------------------

PURPOSE
This lab explains how Windows Scheduled Tasks work, why they are used,
and how their configuration can affect system functionality and security.
It also documents modifying an existing task using the command line.

-----------------------------------------------------------------------

WHAT ARE SCHEDULED TASKS?
Scheduled Tasks are a Windows feature that allows programs or scripts
to run automatically at specific times or when certain events occur.

Common uses:
- Launch scripts or programs
- Automate routine tasks
- Perform system maintenance
- Run backups
- Execute software updates

Open Task Scheduler:
Win + R
taskschd.msc

-----------------------------------------------------------------------

CORE COMPONENTS OF A TASK
When creating or reviewing a task, always check:

- Triggers       : When the task runs
- Actions        : What the task runs
- User Context   : Which account runs the task
- Conditions     : Additional requirements (idle, power, network)
- Settings       : Failure behavior, time limits, expiration

-----------------------------------------------------------------------

TRIGGERS
Triggers define when a task should run.

Examples:
- Time-based (daily, weekly, specific time)
- Event-based (system startup, user logon)

Triggers can be configured to:
- Repeat at intervals
- Delay execution
- Stop after a set duration

-----------------------------------------------------------------------

ACTIONS
Actions define what the task does.

Examples:
- Run a program
- Run a PowerShell script
- Start a service

Example action:
powershell.exe -f C:\Windows\task.ps1

-----------------------------------------------------------------------

CONDITIONS
Conditions define when a task is allowed to run.

Examples:
- Only when the computer is idle
- Only when on AC power
- Only when connected to a specific network

-----------------------------------------------------------------------

SETTINGS
Settings control how the task behaves.

Examples:
- Restart task if it fails
- Stop task if it runs too long
- Delete task after a set time

-----------------------------------------------------------------------

GUI METHOD (TASK SCHEDULER)
Steps to create a basic task:
1. Open Task Scheduler
2. Right-click Task Scheduler Library
3. Select Create Basic Task
4. Enter Name and Description
5. Choose a Trigger
6. Choose an Action
7. Review and finish

Tasks can be edited later:
Right-click task -> Properties

-----------------------------------------------------------------------

COMMAND LINE METHOD (SCHTASKS)

Create a task:
schtasks /create /tn "Task Name" /tr "Action" /sc "Trigger" /ru "Username"

Example:
schtasks /create /tn "My Task" /tr "powershell.exe -f C:\Windows\myscript.ps1" /sc DAILY /ru User

Modify a task:
schtasks /change /tn "Task Name" /tr "New Action"

Delete a task:
schtasks /delete /tn "Task Name"

List all tasks:
schtasks /query

View a specific task:
schtasks /query /tn "Task Name"

-----------------------------------------------------------------------

PARAMETERS QUICK REFERENCE
/tn   Task name
/sc   Schedule or trigger type
/tr   Action (command to run)
/ru   Run-as user account

-----------------------------------------------------------------------

IN THIS LAB (PRACTICAL TASK)
Objective:
Modify the existing scheduled task named "ChangeMe" to run a new script.

Required action:
Run the PowerShell script:
C:\Users\Public\changed.ps1

Command used:
schtasks /change /tn "ChangeMe" /tr "powershell.exe -ExecutionPolicy Bypass -File C:\Users\Public\changed.ps1"

Verification:
schtasks /query /tn "ChangeMe" /v /fo list

Confirm that "Task To Run" shows the updated command.

-----------------------------------------------------------------------

SECURITY NOTES
Scheduled Tasks can pose security risks if misconfigured because they can:
- Run automatically without user interaction
- Execute scripts or binaries silently
- Run under high-privilege accounts

Always review:
- The run-as account
- The action path
- Whether the task runs with highest privileges
- Tasks executing from writable locations (e.g., C:\Users\Public)

-----------------------------------------------------------------------

KEY TAKEAWAYS
- Scheduled Tasks automate system operations
- Misconfigured tasks can introduce security risks
- High-privilege tasks require careful review
- Both GUI and CLI management are important

-----------------------------------------------------------------------

REVISION NOTES
- Always check the user account running the task
- Monitor tasks that execute scripts or binaries
- Avoid unnecessary high-privilege tasks
- Regularly review scheduled tasks for security
