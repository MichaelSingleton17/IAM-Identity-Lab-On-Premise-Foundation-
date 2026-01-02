# Phase 2: Identity Synchronization & Directory Integration

## 📋 Overview
Phase 2 focused on establishing a secure, persistent identity bridge between the on-premises **Active Directory (RTS-DC1)** and the **Okta Identity Cloud**. This phase was critical for enabling automated user lifecycle management and ensuring data integrity across hybrid environments.

## 🛠️ Technical Implementation

### 1. Active Directory Preparation
- **Organizational Unit (OU) Architecture:** Created a dedicated `Okta_Pilot` OU. This allowed for granular control over which objects were synced, ensuring the lab remained within the **10-user limit** of the Okta Integrator Free Plan.
- **Service Account Creation:** Provisioned a least-privilege service account (`OktaService`) to run the AD Agent.
- **Object Population:** Moved 7 pilot users and 3 computer assets into the sync scope.

### 2. Okta AD Agent Deployment
- **Installation:** Deployed the Okta AD Agent on **RTS-DC1**.
- **Connectivity:** Established a secure outbound TLS connection to the Okta tenant.
- **Search Base Configuration:** Limited the agent's visibility to the `OU=Okta_Pilot,DC=internal,DC=sauce,DC=com`.

### 3. Attribute Mapping & Schema
- Mapped key AD attributes to the Okta Universal Directory:
  - `department` → `user.department`
  - `title` → `user.title`
  - `mail` → `user.email`

---

## 🔍 Troubleshooting & Issue Resolution
*The following hurdles were encountered and resolved during the deployment process:*

### **Issue A: Agent Connectivity (Service Error 1067)**
- **Symptom:** The Okta AD Agent service failed to start or stayed in a "Stopped" state.
- **Root Cause:** DNS resolution failure on the Domain Controller. The DC was unable to resolve Okta API endpoints due to missing external forwarders.
- **Resolution:** Configured Google Public DNS (8.8.8.8) as a forwarder in the DNS Manager and verified gateway connectivity.

### **Issue B: LDAP Access Denied**
- **Symptom:** System logs showed `FAILURE: Access is denied` during LDAP read operations.
- **Root Cause:** The `OktaService` account lacked permissions to read the specific `Okta_Pilot` container.
- **Resolution:** Executed the **Delegation of Control Wizard** in ADUC to grant the service account "Read all user information" and "Read all computer information" permissions.

### **Issue C: Data Type Validation (zipCode)**
- **Symptom:** Import failed for specific users with the error `address.zipCode: The field is too long`.
- **Root Cause:** A mismatch between AD string data and Okta's attribute character limits.
- **Resolution:** Sanitized the AD source data and adjusted the Okta Profile Editor mapping to ensure attribute compatibility.

---

## ✅ Final Results
- **Success Rate:** 100% of the targeted 7 pilot users successfully synced.
- **License Status:** 9/10 Active users (Safe within Integrator Free Plan limits).
- **Automation Ready:** Attributes are now correctly populating in Okta, enabling Phase 3 (Group Rules).

---

## 📸 Evidence of Completion
*[Optional: Insert screenshots of your successful Okta Import screen or the 'Running' agent status here]*
