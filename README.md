# nmg-identity-automation
Identity lifecycle automation with PowerShell built during the TotalThreat 30-Day Challenge

# NMG Identity Automation with Powershell

PowerShell tooling for identity lifecycle management, built for a fictional healthcare organization called
Northstar Medical Group.

## The Problem

Northstar Medical Group lacked a reliable way to identify dormant user accounts belonging to former employees.

Prior to April, the offboarding process was managed by a single employee responsible for notifying the appropriate
departments when someone left the organization. Following that employee’s retirement, these notifications stopped, 
leaving the process unmonitored for more than 100 days.

A manual investigation identified 23 dormant accounts and took 11 hours over four days. However, 
the investigation could not reliably determine whether these accounts belonged to former employees 
whose departures had not been recorded, contractors not listed in payroll records, or service accounts not 
associated with individual users.


## The Approach

Rather than comparing directory records against payroll records, the tools developed in this project check the domain controller directly to find the last time each account was used.

## Tools

### Find-StaleAccounts.ps1

Identifies enabled accounts that have not authenticated within a given
number of days, including accounts that have never authenticated.
Exports a timestamped CSV plus a summary recording the exact query used.

    .\Find-StaleAccounts.ps1
    .\Find-StaleAccounts.ps1 -Days 30
    .\Find-StaleAccounts.ps1 -Days 180 -IncludeDisabled

| Parameter | Type | Default | Description |
|---|---|---|---|
| `-Days` | int | 90 | Days without authentication before an account is considered stale |
| `-ReportPath` | string | C:\Reports | Where reports are written |
| `-IncludeDisabled` | switch | off | Include disabled accounts in results |

**Output:** a timestamped CSV of findings, and a summary file recording
the question that produced them so the report can be reproduced.

## Repository Structure

    Scripts/        PowerShell tools
    Documentation/  Runbooks and process documentation
    Evidence/       Sample output and verification screenshots
    Logs/           Execution logs

## Environment

Windows Server with Active Directory Domain Services.
Requires the ActiveDirectory PowerShell module.

## About

Built during the TotalThreat 30-Day Challenge in a simulated
healthcare environment. Northstar Medical Group is fictional.

Author: Elissa Selmore