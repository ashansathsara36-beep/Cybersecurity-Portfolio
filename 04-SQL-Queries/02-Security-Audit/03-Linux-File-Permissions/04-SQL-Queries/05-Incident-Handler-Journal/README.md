# Incident Handler's Journal: Phishing & Brute-Force Response

## 📖 Scenario
I am a Level 1 Security Analyst working in a SOC (Security Operations Center). At 2:15 PM, our SIEM alerted us to multiple failed login attempts for a high-privilege user account, followed by a successful login from a suspicious foreign IP address. I was tasked with triaging this incident, containing the threat, and documenting the response.

## 🎯 Objective
To investigate a potential account compromise, contain the attacker, eradicate the threat, and recover the system while documenting every step in a clear, auditable incident report.

## 🛠️ Tools Used
- SIEM (Splunk / Chronicle)
- Endpoint Detection & Response (EDR)
- Threat Intelligence (VirusTotal, AbuseIPDB)

---

## 📋 Incident Timeline (Play-by-Play)

| Time | Action Taken |
| :--- | :--- |
| **2:15 PM** | SIEM alert triggered: 15 failed login attempts for user `jsmith` from IP `45.33.22.11`. |
| **2:17 PM** | Successful login for `jsmith` from the same IP. Immediate red flag. |
| **2:20 PM** | I escalated the alert to **Critical** and blocked the suspicious IP at the firewall. |
| **2:25 PM** | Force-reset `jsmith`'s password and forced logout of all active sessions. |
| **2:30 PM** | Checked `jsmith`'s email outbox. Found 3 suspicious internal emails sent to the Finance team. Quarantined those emails. |
| **3:00 PM** | Scanned `jsmith`'s workstation using EDR. No malware found, indicating the compromise was purely credential-based. |
| **3:30 PM** | Re-enabled `jsmith`'s account. Escalated the incident to the Lead Analyst for further forensic review. |

---

## 🔍 Root Cause Analysis
- **Vulnerability:** User `jsmith` was using a weak, reused password (`Winter2024!`) that was found in a previous data breach (credential stuffing).
- **The Attack:** The attacker used automated brute-force tools to guess the password, then manually accessed the email to send phishing links to the Finance team.

---

## 🛡️ Containment, Eradication & Recovery

- **Containment:** Blocked IP `45.33.22.11` at the firewall. Disabled the compromised account for 30 minutes.
- **Eradication:** Reset password to a complex 16-character string (including MFA enrollment). Deleted the fraudulent emails from the Finance team's inboxes.
- **Recovery:** Re-enabled the account. Monitored network logs for 2 hours; no further suspicious activity detected.

---

## 📝 Lessons Learned & Recommendations
1. **Implement MFA (Multi-Factor Authentication) immediately** for all administrative users.
2. **Conduct a company-wide training** on identifying phishing emails (the attacker used urgency in the email subject lines).
3. **Implement a password policy** requiring at least 12 characters with complexity (numbers, symbols, uppercase/lowercase).

## 🏁 Outcome
The incident was successfully contained within 1 hour. No data was exfiltrated, and no financial loss occurred. The incident report was filed for compliance review.
