# Comperhensive Plan and Timeline.

## **Phase 1: The Foundation (Active Directory)** 🖥️

**Everything starts with On-Prem Active Directory (AD). It serves as the primary source of truth for many organizations.**

Setup:

OS: 

• Download the Windows Server 2022 Evaluation (180-day free trial).
 
Environment: 

• Run this as a Virtual Machine (VM) using VMware Workstation Player or Oracle VirtualBox.

Configuration:

• Promote the server to a Domain Controller (DC), create a test domain (e.g., lab.local), and set up a few "Organizational Units" (OUs) for Users and Groups.

Key Resources:

• Microsoft Evaluation Center for the ISO.


## **Phase 2: The Cloud Bridge (Entra ID)** ☁️

**Microsoft Entra ID (formerly Azure AD) is the cloud counterpart**

Setup: 

• Sign up for a Microsoft 365 Developer Program account. This gives you a free E5 tenant with 25 licenses for 90 days (renewable if you use it).

• Entra Connect: Download the Entra Connect agent on your AD VM and perform a "Custom Install" to sync your lab.local users to the cloud.

• Key Learning: Practice Password Hash Synchronization (PHS) and Seamless SSO as mentioned in your screenshot.


## **Phase 3: The Identity Hub (Okta)** 🛡️

**Okta acts as the "Universal Directory" and Single Sign-On (SSO) engine.**

Setup:

• Sign up for an Okta Developer Edition account (Free).

• AD Integration: Install the Okta AD Agent on a member server in your AD domain. This allows Okta to see your on-prem users.

• Entra Integration: Connect Okta to your Entra ID tenant using the Office 365 app integration. Configure "Provisioning" so that when you create a user in Okta, it automatically appears in Microsoft 365.

• Key Learning: Master SCIM (System for Cross-domain Identity Management) and Group Pushes.



## **Phase 4: Privileged Access (CyberArk)** 🔐

**CyberArk is the "Vault" for highly sensitive accounts. This is the hardest part to lab because it usually requires a partner license.** 

The Alternative:

• Use CyberArk Privilege Cloud (Trial) if available, or focus on their open-source/developer tools.

Alternative for Home Labs: 

• If you cannot get a CyberArk license, look at HashiCorp Vault (community edition) or Delinea (Secret Server) trials.  They function similarly and teach the same "Privileged Access Management" (PAM) concepts.

Goal: 

• Learn how to "rotate" passwords. When an admin needs to log into the Domain Controller, they must "check out" the password from the Vault rather than knowing it themselves.


## **📅 Project Timeline: 6-Week IAM Home Lab**

Start Date: Dec 28, 2025 | End Date: Feb 8, 2026

<img width="305" height="226" alt="image" src="https://github.com/user-attachments/assets/2eedd6e8-6630-427e-a03e-72dcd2edbb71" />




## **🧱 Phase 1: The Foundation (Active Directory)**

Duration: Dec 28 – Jan 07 (11 Days)

Build Window: Dec 28 – Jan 04 (Setting up VM, Domain Controller, OUs, and Users).

**🛠️ Troubleshooting: Jan 05 – Jan 07 (Fixing DNS issues, Group Policy testing, and VM performance).**

## **☁️ Phase 2: The Cloud Bridge (Entra ID)**

Duration: Jan 08 – Jan 18 (11 Days)

Build Window: Jan 08 – Jan 15 (M365 Developer setup, Entra Connect installation, and PHS sync).

**🛠️ Troubleshooting: Jan 16 – Jan 18 (Resolving sync errors, UPN mismatches, and login failures).**

## **🔄 Phase 3: The Identity Hub (Okta)**

Duration: Jan 19 – Jan 29 (11 Days)

Build Window: Jan 19 – Jan 26 (Okta AD Agent setup, O365 integration, and SCIM provisioning).

**🛠️ Troubleshooting: Jan 27 – Jan 29 (Debugging attribute mapping and Group Push failures).**

## **🔐 Phase 4: Privileged Access (CyberArk / PAM)**

Duration: Jan 30 – Feb 08 (10 Days)

Build Window: Jan 30 – Feb 05 (Vault setup/Trial configuration, rotation policies).

**🛠️ Troubleshooting: Feb 06 – Feb 08 (Final audit, credential rotation fixes, and lab documentation).**
