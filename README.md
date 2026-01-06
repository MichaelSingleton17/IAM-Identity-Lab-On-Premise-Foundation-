# Active Directory Group Policy (GPO) Hardening Documentation

## 📌 Overview
This document outlines the security configurations applied to the `internal.sauce.com` domain. The goal was to transition from default "out-of-the-box" settings to a hardened posture aligned with **NIST SP 800-53** and **DISA STIG** benchmarks.

---

## 🛠️ Implemented GPOs


### 1. NIST Baseline Security Policy
**Objective:** Aligned Active Directory GPOs with NIST SP 800-53 and SP 800-63B standards. 
* **IA-5 (Password Policy):** * Minimum Password Length: **14 Characters**.
    * Password Complexity: Disabled (prioritizing length per NIST 800-63B).
    * Password History: **24 versions** remembered to prevent reuse.
* **AC-11 (Session Lock):** * Inactivity Timeout: **900 seconds (15 minutes)**.
    * Action: Force lock screen/screensaver.
* **IA-4 (Account Lockout):**
    * Threshold: **10 invalid attempts**.
    * Duration: **15 minutes** to mitigate brute-force/dictionary attacks.

### 2. DISA STIG Compliance (DoD Hardening)
**Objective:** Reduce the attack surface and eliminate legacy protocols often exploited in internal pentests.
* **V-205908 (WDigest):** Disabled WDigest authentication to prevent clear-text passwords from residing in LSASS memory.
* **V-205934 (Credential Caching):** Restricted `Interactive Logon: Number of previous logons to cache` to **2**.
* **V-205646 (Legacy Crypto):** Disabled LanMan hash storage to enforce NTLMv2/Kerberos.
* **V-205688 (Legal Notice):** Configured the mandatory DoD Login Banner for all interactive logins.

### 3. Least Privilege & UAC (User Account Control)
**Objective:** Protect the system integrity of workstations in the `Okta_Pilot` OUs.
* **UAC Behavior:** Configured to "Prompt for consent on the secure desktop" for Administrators.
* **Standard User Elevation:** Forced credential entry for all elevation requests.
* **Control Panel Restriction:** Prohibited access for `Sales_Apps`, `Engineering_Apps`, `Finance_Apps`, `Service_Apps` groups to prevent unauthorized system changes.

### 4. 🛡️ UAC & System Integrity (NIST AC-6)
**Objective:** Implemented User Account Control (UAC) policies to enforce the "Secure Desktop" boundary:
- Configured **Admin Approval Mode** to ensure all administrative tasks require explicit consent.
- Forced **Standard User Elevation** to require credential entry, preventing unauthorized software installations in the `Okta_Pilot` OUs.

---

## 🔍 Verification & Audit
To verify the application of these policies across the domain, the following commands were utilized on pilot workstations:

| Command | Purpose |
| :--- | :--- |
| `gpupdate /force` | Immediate refresh of Group Policy settings. |
| `gpresult /r` | Visual confirmation of applied GPOs for the current user/computer. |
| `rsop.msc` | Resultant Set of Policy tool to troubleshoot conflicting settings. |

---

## 📈 Impact on Identity Bridge
These GPOs complement the **Okta AD Agent** by ensuring that while Okta handles the "Front Door" (Cloud SSO), the "Internal Doors" (Local OS) are locked and monitored according to federal standards.
