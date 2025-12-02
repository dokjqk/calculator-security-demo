# Scanner Comparison

## Only CodeQL (SAST) Found

### Flask App Is Run in Debug Mode  
**Severity:** High  
**Detected by:** CodeQL  
**Location:** `app.py:40`
**Details:** Running a Flask application with debug mode enabled may allow an attacker to gain access through the Werkzeug debugger.



## Only ZAP (DAST) Found

### Summary of Alerts
| **Risk Level** | **Count** |
|----------------|-----------|
| **High**       | 0         |
| **Medium**     | 3         |
| **Low**        | 4         |

---

### Medium-Risk Findings
- **Content Security Policy (CSP) Header Not Set**
- **HTTP Only Site**
- **Missing Anti-Clickjacking Header**

---

### Low-Risk Findings
- **Insufficient Site Isolation Against Spectre Vulnerability**
- **Permissions Policy Header Not Set**
- **Server Version Information Exposed (`Server` HTTP header)**
- **X-Content-Type-Options Header Missing**

---

### Informational Findings
- **Modern Web Application**
- **Sec-Fetch-**



## Only Dependency-Check (SCA) Found
- **0 vulnerable dependencies**
