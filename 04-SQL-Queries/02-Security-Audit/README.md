# Botium Toys Security Audit Report

**Date:** June 2026  
**Auditor:** [Your Name]  
**Client:** Botium Toys (Owner: Mae)  
**Framework:** NIST Cybersecurity Framework (CSF) & CIS Controls v8

---

## 1. Executive Summary
Botium Toys is a rapidly growing e-commerce toy retailer. Currently, the company operates with a minimal security infrastructure. This audit identifies critical gaps in asset management, access control, and data encryption. Immediate action is required to protect customer Personally Identifiable Information (PII) and maintain business continuity.

---

## 2. Scope of Audit
The audit covered the following areas:
- **Internal Network:** Workstations, servers, and internal Wi-Fi.
- **E-commerce Platform:** Customer database, payment processing, and web hosting.
- **Employee Practices:** Password policies, remote access, and device management.
- **Policies:** Incident response, disaster recovery, and data retention.

---

## 3. Current Asset Inventory (Mapped)
| Asset Type | Description | Owner |
| :--- | :--- | :--- |
| **Workstations** | 15 Windows laptops for employees | IT Team |
| **Web Server** | Hosts the company website and customer portal | External Hosting Provider |
| **Database Server** | Stores customer names, addresses, and credit card hashes | Internal IT |
| **Network Firewall** | Basic router with NAT | ISP Provided |
| **Software** | Windows 10, Office 365, Custom POS System | IT Team |

---

## 4. Risk Assessment & Vulnerabilities

### Critical Vulnerabilities:
1. **Missing Asset Inventory:** No formal tracking of all hardware/devices connected to the network.
2. **Lack of Least Privilege:** All 15 employees have administrative access to the financial database.
3. **No Encryption:** Customer credit card data is transmitted and stored in plaintext (no SSL/TLS or disk encryption).
4. **No MFA (Multi-Factor Authentication):** Employees access sensitive systems using only a username and password.
5. **No Incident Response Plan:** The company has no written plan to follow during a data breach.

---

## 5. Compliance Checks

### PCI-DSS (Payment Card Industry) Compliance:
| Requirement | Status | Notes |
| :--- | :--- | :--- |
| Protect Cardholder Data | ❌ **Fail** | No encryption on customer credit card data. |
| Maintain Vulnerability Program | ⚠️ Partial | Basic antivirus installed, but no patching policy. |
| Implement Strong Access Control | ❌ **Fail** | No restriction on which employees can see financial data. |

### GDPR / CCPA (Data Privacy) Compliance:
| Requirement | Status | Notes |
| :--- | :--- | :--- |
| Right to Data Erasure | ❌ **Fail** | No process to delete customer data upon request. |
| Data Breach Notification | ❌ **Fail** | No process to notify customers within 72 hours. |

---

## 6. Action Plan & Recommendations

| Priority | Recommendation | Timeline |
| :--- | :--- | :--- |
| **Critical** | Implement encryption (SSL/TLS for website, AES-256 for hard drives). | 1 Week |
| **Critical** | Implement Least Privilege (Restrict financial data access to the accounting team). | 3 Days |
| **High** | Deploy MFA for all employee accounts. | 2 Weeks |
| **High** | Document an Incident Response Plan. | 1 Month |
| **Medium** | Conduct a full physical hardware inventory audit. | 1 Month |
| **Low** | Schedule annual security awareness training for all employees. | 3 Months |

---

## 7. Conclusion
Botium Toys is operating at a high risk of a data breach. The lack of encryption and access controls makes them an attractive target for cybercriminals. 

**Recommendation:** Implement the Critical and High-priority recommendations within the next 30 days to significantly reduce risk. A follow-up audit is strongly recommended within 6 months.

---

**Approved By:**  
__________________________  
Mae (Owner, Botium Toys)  
Date: _______________
