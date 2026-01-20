Lab 1: Windows Services Fundamentals
Objective

Understand how Windows services operate, how they are configured,
and how service execution context affects system security.

Tools Used

Windows Services Management Console (services.msc)

Windows built-in service configuration utilities

Key Concepts

Background service execution in Windows

Service startup types (Automatic, Manual, Disabled)

Service execution context and privilege levels

Security implications of unnecessary or misconfigured services

Principle of least privilege

Service Analysis Example

Service Name: DNS Client
Service Identifier: Dnscache

Analysis Method

The service configuration was examined using the Windows Services
management console. The execution context was identified through the
Log On tab in the service properties.

Execution Context

Runs under: NT AUTHORITY\NetworkService

Security Observations

Uses a restricted built-in account

Limits system access compared to administrative accounts

Helps reduce the impact of potential service compromise

Learning Outcome

This lab demonstrates how proper service configuration supports
system security and stability, and why understanding service privileges
is essential in Windows security administration.
