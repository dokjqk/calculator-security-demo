# Security Policy

This repository uses automated security scanning to detect vulnerabilities in the source code, dependencies, and the running application.  
Below is an overview of the tools, when they run, what they cover, and how to read their results.

---

# 🔒 Security Scanning Overview

This project uses **three layers of security scanning**:

1. **SAST — Static Application Security Testing (CodeQL)**
2. **SCA — Software Composition Analysis (Dependency-Check)**
3. **DAST — Dynamic Application Security Testing (OWASP ZAP)**

Each scanner looks at a different part of the application and complements the others.

---

# 🧪 Scanning Tools

## 1. CodeQL (SAST)
**What it does:**  
- Analyzes source code for insecure patterns and logic issues  
- Finds vulnerabilities such as unsafe input handling, debug mode, resource misuse, etc.

**Triggers:**  
- Runs on every push and pull request to `main`

**Covers:**  
- Python code in the repository  
- Data-flow vulnerabilities  
- High-risk code configurations  

**Example Finding (from your scan):**
- **Flask app is run in debug mode**  
  - *Severity:* High  
  - *Location:* `app.py:40`  
  - *Details:* Debug mode exposes Werkzeug debugger which may allow execution of arbitrary code.

**Workflow File:**  
`/.github/workflows/codeql-analysis.yml`

---

## 2. Dependency-Check (SCA)
**What it does:**  
- Analyzes project dependencies  
- Detects known CVEs in libraries  

**Triggers:**  
- Runs on push to `main`

**Covers:**  
- Python packages listed in `requirements.txt`

**Example Finding (from your scan):**
- **0 vulnerable dependencies**

**Artifacts:**  
- `sca-reports/`

**Workflow File:**  
`/.github/workflows/dependency-check.yml`

---

## 3. OWASP ZAP (DAST)
**What it does:**  
- Scans the *running* web application  
- Detects missing security headers, unsafe configurations, and exposed endpoints

**Triggers:**  
- Runs on push to `main`
- Two modes:
  - **Baseline Scan** (passive)
  - **Full Scan** (active)

**Covers:**  
- Server responses  
- Security headers  
- Runtime web behavior  

### Summary of DAST Findings  
| **Risk Level** | **Count** |
|----------------|-----------|
| **High**       | 0         |
| **Medium**     | 3         |
| **Low**        | 4         |

### Medium-Risk Issues
- Content Security Policy (CSP) Header Not Set  
- HTTP Only Site  
- Missing Anti-Clickjacking Header  

### Low-Risk Issues
- Insufficient Site Isolation Against Spectre  
- Permissions Policy Header Not Set  
- Server Version Exposed  
- X-Content-Type-Options Missing  

### Informational
- Missing Sec-Fetch-* headers  
- Storable and Cacheable Content  

**Artifacts:**  
- `zap-baseline-reports/`  
- `zap-fullscan-reports/`

**Workflow Files:**  
- `/.github/workflows/zap-baseline.yml`  
- `/.github/workflows/zap-fullscan.yml`

---

# 📘 How to Interpret Results

### CodeQL (SAST)
- Look for “High” or “Critical” severity issues  
- Fix misconfigurations (e.g., debug mode)  
- Review data-flow warnings (unsafe input handling)

### Dependency-Check (SCA)
- Review CVEs in the generated HTML/JSON reports  
- Update affected packages  
- Re-run scan after updating dependencies

### ZAP (DAST)
- Medium+ findings usually indicate missing security headers  
- Low findings are informational but still good to fix  
- Full-scan results reveal potential runtime vulnerabilities

---

# 🛡 Reporting Vulnerabilities

If you discover a security issue:

1. **Do not publicly disclose it.**  
2. Email the security contact for this repo:  
   **security@example.com**  
3. Provide:
   - Steps to reproduce  
   - Severity (if known)  
   - Files or endpoints affected  

---

If you’d like, I can also turn this into a fully polished **README Security Section**, or generate a **SCAN_ANALYSIS.md** using all of your results.
