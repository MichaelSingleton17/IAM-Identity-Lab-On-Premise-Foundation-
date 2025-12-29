# IAM Identity Lab: On-Premise Foundation (Phase 1)

## Architecture Overview
- **Domain Controller:** RTS-DC1 (Windows Server 2022)
- **Domain Name:** internal.sauce.com
- **Static IP:** 172.16.10.10

## Implementation Highlights
- **Bulk Identity Creation:** Generated 92 active users using PowerShell automation.
- **Data Enrichment:** Populated critical attributes (Email, Department, Title, Manager) to support Attribute-Based Access Control (ABAC).
- **Security Posture:** Implemented a Least Privilege service account (`svc-okta`) for future cloud integration.

## Compliance Mapping
- **NIST SP 800-63B:** Enrollment and Identity Lifecycle Management.
- **NIST SP 800-53 (AC-2):** Account Management and Organizational Unit (OU) structuring.

## Project Overview
This lab is designed to simulate an enterprise identity environment to practice IAM integration with Okta, Entra ID, and CyberArk.

## Phase 1 Architecture
- **Domain Controller:** RTS-DC1 (Windows Server 2022)
- **Domain:** internal.sauce.com
- **Network:** 172.16.10.10 (Static IP)

## Identity Data Summary
- **Total Active Users:** 92
- **Organizational Units (OUs):** Corporate_Users, Sales, Engineering, Service_Accounts, Finance.
- **Data Enrichment:** All users have populated attributes for Email, Department, Title, and Manager to support Attribute-Based Access Control (ABAC).

## Scripts Included
- `Build-OUs.ps1`: Creates the hierarchical OU structure.
- `Bulk-User-Creation.ps1`: Generates 92 test users with randomized data.
- `Enrich-Identity-Data.ps1`: Updates user attributes (Department, Manager) based on OU placement.
