# SQL Queries: Filtering for Security Threats

## 📖 Scenario
I am a security analyst at a large e-commerce company. I need to investigate suspicious login activity and potential data breaches. Using a database of employee logins and failed authentication attempts, I must write SQL queries to filter out specific patterns and identify anomalies.

## 🎯 Objective
To use SQL `SELECT` and `WHERE` clauses with logical operators to filter security logs, identify failed login attempts from suspicious IP addresses, and locate high-risk user accounts.

## 🛠️ Tools Used
- SQL (MySQL / MariaDB syntax)
- Database: `security_logs` and `employees` tables
- Operators: `AND`, `OR`, `LIKE`, `BETWEEN`, `ORDER BY`

---

## 🔍 Query 1: Identify Failed Login Attempts
The security team wants a list of all failed login attempts that occurred after business hours (6:00 PM).

### Command Entered:
```sql
SELECT *
FROM security_logs
WHERE login_status = 'failed' 
  AND login_time > '18:00:00';
```

### Output Received (Simulated):
```sql
+----+---------+----------------+----------------+-----------+
| id | user_id | login_time     | ip_address     | status    |
+----+---------+----------------+----------------+-----------+
| 45 | 1023    | 2026-06-15 22:15 | 192.168.1.45  | failed    |
| 78 | 2056    | 2026-06-16 19:30 | 10.0.0.89     | failed    |
+----+---------+----------------+----------------+-----------+
```

> **Analysis:** Both login attempts occurred late at night. These could indicate brute-force attacks or unauthorized access attempts.

---

## 🔍 Query 2: Identify Suspicious IP Addresses
The SOC team flagged the IP address range `192.168.1.0/24`. I need to pull all login attempts (both success and failure) originating from this subnet.

### Command Entered:
```sql
SELECT user_id, login_time, ip_address, login_status
FROM security_logs
WHERE ip_address LIKE '192.168.1.%';
```

### Output Received (Simulated):
```sql
+---------+----------------+----------------+--------------+
| user_id | login_time     | ip_address     | login_status |
+---------+----------------+----------------+--------------+
| 1023    | 2026-06-15 22:15 | 192.168.1.45  | failed       |
| 1023    | 2026-06-15 22:17 | 192.168.1.45  | success      |
+---------+----------------+----------------+--------------+
```

> **Analysis:** User `1023` had a failed attempt followed by a successful one two minutes later from the same suspicious IP. This may indicate a compromised account.

---

## 🔍 Query 3: Locate High-Risk Employees
Management wants a list of all employees in the Finance and IT departments to conduct a targeted security training session.

### Command Entered:
```sql
SELECT employee_id, full_name, email, department
FROM employees
WHERE department = 'Finance' 
   OR department = 'IT';
```

### Output Received (Simulated):
```sql
+-------------+----------------+----------------------+------------+
| employee_id | full_name      | email                | department |
+-------------+----------------+----------------------+------------+
| 2056        | Sarah Johnson  | sarah.j@company.com  | IT         |
| 3021        | Mike Chen      | mike.c@company.com   | Finance    |
+-------------+----------------+----------------------+------------+
```

> **Analysis:** These users have access to highly sensitive financial and infrastructure systems. Targeted training will help mitigate social engineering risks.

---

## 📚 Summary of SQL Filters Used
| SQL Command | Purpose |
| :--- | :--- |
| `WHERE login_status = 'failed'` | Filters for failed login attempts. |
| `AND login_time > '18:00:00'` | Adds a time-based filter. |
| `LIKE '192.168.1.%'` | Uses wildcards to search for IP subnets. |
| `OR` | Combines multiple condition filters. |

## 🏁 Outcome
Successfully extracted actionable security intelligence from the database. These queries can be automated into daily threat-hunting reports to detect brute-force patterns, compromised accounts, and high-risk user groups proactively.
