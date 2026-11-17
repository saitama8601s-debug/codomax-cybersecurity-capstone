# codomax-cybersecurity-capstone
# SecGuard SIEM — Security Log Analyzer & Threat Dashboard (Capstone Project)

**Intern Name:** Akshat Dave  
**Program:** Codomax Cybersecurity Virtual Internship (Module 06 — Capstone)  
**Scope:** Authorized local/client-side log parsing and threat detection simulation.

---

## 1. Project Overview & Security Architecture
**SecGuard SIEM** is a lightweight, browser-based Security Log Analyzer and Threat Detection Dashboard designed to parse authentication, web server, and privilege-escalation logs in real time without transmitting sensitive telemetry to external servers.

### Architecture Flow
1. **Log Ingestion Layer:** Accepts raw syslog, OpenSSH (`auth.log`), and Nginx/Apache HTTP access logs via client-side input.
2. **Detection & Correlation Engine:** Evaluates each log entry against regex-based detection signatures mapped to MITRE ATT&CK and OWASP Top 10 categories (SSH Brute Force, SQL Injection, Cross-Site Scripting, and Suspicious Command Execution).
3. **Entity Extraction Module:** Extracts source IPv4 indicators (`IoCs`) and aggregates alert severity metrics (`HIGH`, `MEDIUM`, `LOW`).
4. **Incident Response Guidance:** Maps each detected anomaly to actionable Blue Team containment and hardening steps.

---

## 2. Testing Report & Validation Matrix

| Test Case ID | Simulated Log Input | Expected Detection | Result | Status |
| :--- | :--- | :--- | :--- | :--- |
| **TC-01** | `Failed password for root from 203.0.113.45` | SSH Brute-Force Attempt (`HIGH`) | Flagged `HIGH`, extracted IP `203.0.113.45` | **PASS** |
| **TC-02** | `GET /login.php?user=admin' OR '1'='1' --` | SQL Injection Probe (`HIGH`) | Flagged `HIGH`, mapped to WAF/Prepared Statement fix | **PASS** |
| **TC-03** | `GET /search?q=<script>alert(1)</script>` | Reflected XSS Payload (`MEDIUM`) | Flagged `MEDIUM`, safely escaped HTML output | **PASS** |
| **TC-04** | `sudo: deploy : COMMAND=/usr/bin/curl http://...` | Unauthorized C2 Download (`HIGH`) | Flagged `HIGH`, recommended EDR host isolation | **PASS** |
| **TC-05** | `systemd[1]: Started Daily apt download` | Normal System Event (`LOW`) | Classified `LOW` with zero false-positive escalation | **PASS** |

---

## 3. Demo Walkthrough
1. Open the Live Website URL hosted via GitHub Pages.
2. On initial load, **Load Sample Attack Logs** automatically populates realistic multi-vector attack logs and renders KPI counters (`Total Events`, `High/Critical Alerts`, `Suspicious IPs`, and `System Status`).
3. Paste custom server logs into the input console and click **Analyze Logs** to classify threats and review remediation steps.
