
## ** 🛡️ IAM Security Lab & Infrastructure Engineering **

Powered by the USET Framework (Users, Security, Environment, Trust)
This repository documents the end-to-end deployment of a hybrid IAM environment, focusing on the seamless integration of Active Directory and Okta, while maintaining infrastructure resilience through advanced hardware optimization.
________________________________________
🏛️ The USET Framework Methodology
Developed to move beyond technical execution into structured enterprise strategy, the USET Framework guides every implementation in this lab.
• Users: Centralized identity lifecycle management.
• Security: Hardening via CASB and PAM agents.
• Environment: Decoupled storage architecture using Directory Junctions.
• Trust: Automated backups and transparent documentation.
________________________________________
🛠️ Configuration & Implementation
1. Identity & Access Management (Software)
• Source of Truth: Windows Server Active Directory.
• Cloud Gateway: Okta Developer Tenant.
• Integration: Established a secure SAML/SCIM handshake for seamless user provisioning.
• Privileged Access: Deployed a PAM Agent in AD to govern administrative accounts.
• Cloud Security: Implemented an Okta CASB Agent to monitor and secure SaaS traffic.
2. Infrastructure Optimization (Hardware)
To prevent system instability during high-traffic Docker and WSL2 operations, I implemented a Storage Bridge architecture.
• System Drive (C:): 250GB SSD (Optimized for OS/App binaries).
• Storage Drive (D:): 1TB HDD (Data, VHDX, and Logs).
• Technical Solution: Used Directory Junctions to redirect the following high-growth directories to the $D$ drive:
o %LocalAppData%\Docker\wsl
o C:\ProgramData\Okta\CASB\Logs
o C:\Program Files\PAM_Agent\Logs
________________________________________
🔍 Troubleshooting & Incident Log
As a QA Security Analyst, I treat every error as a data point for system hardening.
Issue	Root Cause	Resolution	Framework Pillar
0-Byte Free Space (C:)	Docker/WSL2 VHDX expansion on system drive.	Established Directory Junctions to 1TB HDD.	Environment
WSL Permission Denied	Sharing violation during file migration.	Corrected root@Sauce ownership via chown.	Security
Agent Command Not Found	PowerShell cmdlet execution in CMD environment.	Migrated automation to PS Admin shell.	Environment
Potential Data Loss	Single-point-of-failure on local Git repos.	Automated a weekly Robocopy mirroring script.	Trust
________________________________________
🚀 Automation & Scripts
The lab is maintained via a set of custom PowerShell scripts:
• Weekly_Backup.ps1: Mirrors Github directories to the $D$ drive.
• Storage_Bridge_Setup.ps1: Automates the creation of junctions for new security agents.
