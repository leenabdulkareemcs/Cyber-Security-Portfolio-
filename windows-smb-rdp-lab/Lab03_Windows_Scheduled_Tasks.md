# Lab 03 – Windows Scheduled Tasks  
**Cyber Fundamentals | Windows Basics**

---

## Purpose

This lab focuses on understanding how Windows Scheduled Tasks work, why they are used, and how their configuration impacts system functionality and security.

---

## What Are Scheduled Tasks?

Scheduled Tasks are a Windows system feature that allows users to run files at specific times or when certain events occur.

They are commonly used to:
- Launch scripts or programs  
- Automate routine tasks  
- Perform system maintenance  
- Run backups  
- Execute software updates  

You can access the Task Scheduler by searching for it in the Windows Start menu.

---

## Task Creation Components

When creating a task, you need to specify:

- **Triggers** – What causes the task to run  
- **Actions** – What the task will do  
- **User** – The user account under which the task runs  
- **Conditions** – When the task is allowed to run  
- **Settings** – How the task behaves under certain situations  

---

## Triggers

Triggers define when a task should run.

Examples:
- Time-based (e.g., at 12:00)
- Event-based (e.g., at system startup)

Triggers can also be customized so tasks can be:
- Repeated  
- Delayed  
- Stopped based on a schedule  

---

## Actions

Actions define what a task does.

Examples:
- Running a script  
- Launching a program  
- Starting a service  

---

## Conditions

Conditions specify when a task is allowed to run.

Examples:
- Only when the computer is idle  
- Only when on AC power  
- Only when connected to a specific network  

---

## Settings

Settings allow fine control over task behavior.

Examples:
- Restart the task if it fails  
- Stop the task if it runs longer than a set time  
- Delete the task after a certain number of days  

---

## Creating a Task (GUI)

A Basic Task uses minimal configuration and a guided wizard.

Steps:
1. Open **Task Scheduler**
2. Right-click **Task Scheduler Library**
3. Select **Create Basic Task**
4. Enter Name and Description
5. Choose a Trigger
6. Choose an Action
7. Review and click Finish

Example action:
```bash
powershell.exe -f C:\Windows\task.ps1
```

You can edit tasks later by right-clicking and selecting **Properties**.

---

## Creating Tasks Using schtasks

You can also manage tasks via command line using **schtasks**.

### Create a Task

```bash
schtasks /create /tn "Task Name" /tr "Action" /sc "Trigger" /ru "Username"
```

Example:
```bash
schtasks /create /tn "My Task" /tr "powershell.exe -f C:\Windows\myscript.ps1" /sc DAILY /ru User
```

---

## Modifying Tasks

Change a task:
```bash
schtasks /change /tn "Task Name" /tr "New Action"
```

Delete a task:
```bash
schtasks /delete /tn "Task Name"
```

---

## Listing Tasks

List all tasks:
```bash
schtasks /query
```

View a specific task:
```bash
schtasks /query /tn "Task Name"
```

---

## Parameters Explained

- **tn** – Specifies the task name  
- **sc** – Specifies the trigger condition  
- **tr** – Specifies the action  
- **ru** – Specifies the user account  

---

## In This Lab

You will:
- Create scheduled tasks  
- Modify existing tasks  
- Delete tasks  
- Use both GUI and schtasks  
- Compare their usage and behavior  

---

## Key Takeaways

- Scheduled Tasks automate system operations  
- Misconfigured tasks can pose security risks  
- Tasks can run with high privileges  
- Both GUI and CLI tools are important to know  

---

## Revision Notes

- Always check the user account running the task  
- Monitor tasks that execute scripts or binaries  
- Avoid unnecessary high-privilege tasks  
- Regularly review scheduled tasks for security
