# Tutorial: Automating F5 Load Balancer Tasks with PowerShell

## Overview

This tutorial walks through automating a common F5 load balancer task — forcing a server offline — using PowerShell and SSH.  
It demonstrates scripting basics, automation workflow, and verification steps.

**Audience:** System administrators, support engineers  
**Skill Level:** Intermediate  

---

## Prerequisites

- PowerShell 5.1 or later  
- SSH access to the F5 load balancer  
- Appropriate permissions to manage pool members  

---

## Steps

1. Connect to the F5 via SSH  
2. Run the PowerShell script to force a server offline  
3. Verify the server status  
4. Bring the server back online (if needed)  

---

## Example Script

```powershell
$server = "10.0.0.5"
$pool = "web_pool"

ssh admin@f5 "tmsh modify ltm pool $pool members modify { $server:80 { session user-disabled } }"

