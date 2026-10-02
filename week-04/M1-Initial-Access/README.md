# M1 — Initial Access

## Mediroza General Hospital Web Application Penetration Test

> **Networkwalks — Week 4 | Authorized Security Lab**

### Objective

The objective of Milestone 1 was to identify an attack path into the Mediroza General Hospital patient portal and retrieve the **three confidential patient PDF laboratory reports** specified by the project brief.

The project brief explicitly authorizes black-box testing of `https://medirozahospital.com` within the agreed scope. fileciteturn4file1

---

## Scope

| Item | Details |
|---|---|
| Client | Mediroza General Hospital |
| Target | `https://medirozahospital.com` |
| Assessment | Black-box penetration test |
| Environment | Kali Linux |
| Milestone | M1 — Initial Access |
| Objective | Retrieve 3 confidential patient PDF reports |

The engagement rules restricted testing to the target domain and prohibited social engineering, denial-of-service activity, and out-of-scope testing. fileciteturn4file1

---

## Methodology

The assessment followed a controlled external testing workflow:

1. DNS and domain reconnaissance
2. Web technology identification
3. Service enumeration
4. Web content discovery
5. `robots.txt` analysis
6. Patient portal discovery
7. Authentication/input testing
8. Controlled exploitation of the identified authentication weakness
9. Verification of authenticated access
10. Retrieval of the three assigned PDF reports

---

## Reconnaissance

The target was first enumerated to identify its publicly exposed attack surface.

### Key observations

- Target resolved to a publicly reachable web server.
- Web technologies and HTTP behavior were fingerprinted.
- Multiple network services were identified during enumeration.
- `robots.txt` disclosed application paths including:

```text
/patient/
/staff/
/old/
```

The `/patient/` path was particularly relevant to the M1 objective.

---

## Patient Portal Discovery

The `/patient/` application exposed the following relevant resources:

```text
/patient/
├── reports/
├── download.php
├── error_log
├── login.php
├── logout.php
└── portal.php
```

The authentication page accepted username and password parameters.

During controlled input testing, the username parameter was tested for SQL-injection behavior. The evidence collected during the lab demonstrated successful access to the restricted patient portal.

> **Evidence:** Keep the original authentication-testing screenshot in the `evidence/` directory. Do not publish real credentials or session cookies.

---

## Successful Access

After successful authentication, the patient portal displayed the assigned laboratory reports under **My Lab Reports**.

Three encrypted pathology reports were identified:

| Report | Lab Reference | Status |
|---|---|---|
| Pathology Report — S. Dlamini | LR-2024-1187 | PDF encrypted |
| Pathology Report — P. Reddy | LR-2024-1192 | PDF encrypted |
| Pathology Report — E. Thompson | LR-2024-1205 | PDF encrypted |

The project brief requires proof of access and retrieval of all three reports. fileciteturn4file7

---

## Evidence

Recommended evidence filenames:

```text
evidence/
├── patient-login.png
├── patient-portal.png
├── report-1-download.png
├── report-2-download.png
└── report-3-download.png
```

### Evidence description

**Patient Login**

Shows the patient portal authentication interface and controlled input testing.

**Authenticated Patient Portal**

Shows successful access to the restricted portal and the three assigned encrypted reports.

**Report Retrieval**

Shows successful retrieval of the three PDF files required by M1.

---

## Impact

Successful exploitation resulted in unauthorized access to a restricted patient-facing application area and exposure of confidential laboratory documents.

Because the affected application handles healthcare information, unauthorized access can create significant confidentiality and privacy risk.

---

## Risk Assessment

**Severity: High**

The milestone demonstrated that a weakness in the authentication/input-handling layer could be used to reach protected patient resources.

The severity is based on:

- Authentication control bypass
- Access to confidential patient documents
- Exposure of healthcare-related information
- Potential for broader unauthorized application access

---

## Recommended Remediation

### 1. Use parameterized database queries

Replace dynamically constructed SQL statements with prepared statements / parameterized queries.

### 2. Validate and constrain user input

Apply server-side input validation and reject unexpected syntax.

### 3. Implement secure authentication

Use:

- Secure password hashing
- Rate limiting
- Account lockout controls
- Secure session management
- MFA where appropriate

### 4. Improve error handling

Authentication responses should avoid revealing database or account-state information.

### 5. Add security regression tests

Include automated SQL-injection and authentication-bypass tests in the application security pipeline.

---

## M1 Result

**Milestone 1 — Completed**

The assessment successfully demonstrated access to the patient portal and retrieval of the three confidential PDF laboratory reports required by the project.

---

## Responsible Disclosure

This repository should contain **redacted evidence only**.

Do not commit:

- Patient medical records
- Patient IDs
- Birth dates
- Medical test results
- Session cookies
- Credentials
- Authentication tokens
- Unredacted screenshots

This module is intended to document the authorized educational security assessment, not to expose real personal information.
