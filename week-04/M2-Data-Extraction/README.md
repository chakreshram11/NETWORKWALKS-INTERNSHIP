# M2 — Data Extraction

## Mediroza General Hospital Web Application Penetration Test

> **Networkwalks — Week 4 | Authorized Security Lab**

### Objective

Milestone 2 required the tester to **crack the encryption on all three retrieved patient PDF files** and provide proof of successful access. The project brief specifically instructs the tester to analyze the encryption, select suitable tools/wordlists, and recover the contents. fileciteturn4file4

---

## Scope

| Item | Details |
|---|---|
| Client | Mediroza General Hospital |
| Target | `https://medirozahospital.com` |
| Milestone | M2 — Data Extraction |
| Input | Three password-protected PDF reports |
| Platform | Kali Linux |
| Primary tools | `pdf2john`, John the Ripper |

---

## Methodology

The following workflow was used:

```text
Retrieved PDF
     │
     ▼
pdf2john
     │
     ▼
PDF password hash
     │
     ▼
John the Ripper
     │
     ▼
Dictionary attack
     │
     ▼
Recovered password
     │
     ▼
PDF opened successfully
```

---

## Step 1 — Extract the PDF Hash

John the Ripper's `pdf2john` utility was used to convert the protected PDF into a password-cracking format.

Example:

```bash
pdf2john patient_report_1.pdf > pdf1.txt
```

For the second report:

```bash
pdf2john patient_report_2.pdf > pdf2.txt
```

For the third report:

```bash
pdf2john patient_report_3.pdf > pdf3.txt
```

The resulting files contain the `$pdf$...` representation required by John the Ripper.

---

## Step 2 — Dictionary Attack

A dictionary attack was performed using the Kali Linux `rockyou.txt` wordlist.

Example:

```bash
john --format=PDF --wordlist=/usr/share/wordlists/rockyou.txt pdf1.txt
```

Repeat for the other reports:

```bash
john --format=PDF --wordlist=/usr/share/wordlists/rockyou.txt pdf2.txt
john --format=PDF --wordlist=/usr/share/wordlists/rockyou.txt pdf3-fixed.txt
```

### Third PDF hash compatibility note

During testing, the third PDF produced a permissions value of:

```text
4294967292
```

The extracted hash was normalized to the signed representation expected by the installed John format:

```text
-4
```

The original extracted hash was retained as evidence, while the normalized copy was used for cracking.

---

## Recovered Passwords

The authorized lab evidence demonstrated successful recovery of all three PDF passwords.

| Report | Password recovery | Verification |
|---|---|---|
| `patient_report_1.pdf` | Recovered | PDF opened |
| `patient_report_2.pdf` | Recovered | PDF opened |
| `patient_report_3.pdf` | Recovered | PDF opened |

> **Security note:** Actual recovered passwords should not be committed to a public GitHub repository. Keep them only in the restricted assessment report/evidence package.

---

## Verification

After recovery, each PDF was opened using its recovered password to verify that the password was valid and the encrypted document could be accessed.

Recommended evidence:

```text
evidence/
├── pdf1-hash.png
├── pdf2-hash.png
├── pdf3-hash.png
├── pdf1-cracked.png
├── pdf2-cracked.png
├── pdf3-cracked.png
├── pdf1-opened.png
├── pdf2-opened.png
└── pdf3-opened.png
```

---

## Finding

### Weak and Predictable PDF Passwords

The PDFs were protected by encryption, but the passwords were sufficiently predictable to be recovered using dictionary-based password auditing.

This demonstrates an important security distinction:

> Strong document encryption does not provide strong practical protection when weak passwords are used.

---

## Impact

An attacker who obtains the encrypted PDF files may be able to recover their passwords through offline password cracking.

Potential impact includes:

- Unauthorized access to confidential laboratory reports
- Exposure of patient information
- Privacy violations
- Increased risk from reused passwords
- Potential regulatory/data-protection consequences

---

## Risk Rating

**Severity: High**

The finding is rated High because confidential healthcare documents could be accessed after offline password recovery.

---

## Recommended Remediation

### 1. Use strong random passwords

Generate long, unique, randomly generated secrets for each document.

### 2. Do not use dictionary passwords

Avoid:

```text
password
123456
qwerty
```

and similar predictable values.

### 3. Prefer authenticated document delivery

Where possible, serve reports through the authenticated patient portal instead of relying solely on PDF passwords.

### 4. Use short-lived access controls

Consider:

- Session-based access
- Expiring download links
- One-time tokens
- MFA
- Access logging

### 5. Prevent password reuse

Each report should use an independent secret.

---

## M2 Result

**Milestone 2 — Completed**

All three assigned encrypted patient PDF reports were successfully processed, their passwords recovered, and the documents opened for verification.

---

## Responsible Disclosure

Do not publish:

- Recovered passwords
- Unredacted patient reports
- Patient IDs
- Medical results
- Birth dates
- Personal information

Use screenshots showing only the minimum evidence necessary to demonstrate successful completion.
