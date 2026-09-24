# NetworkWalks Cybersecurity Internship — Week 3

## Password Cracking & Hash Analysis Lab

This repository documents my **Week 3 project work** completed as part of the **NetworkWalks Cybersecurity Internship**.

The official Week 3 project sheet lists two mandatory modules:

- **W3-PM1 — Password Cracking with JTR (John the Ripper)**
- **W3-PM2 — Password Cracking with NW Tools**

The Week 3 project document states that both essential modules were required. fileciteturn0file0L7-L16

> **Scope:** All password-recovery activities documented here were performed against the provided training PDFs in the controlled internship lab environment.

---

## 1. Objectives

- Understand how password-protected PDF files can be assessed for password recovery.
- Extract PDF password hashes using `pdf2john`.
- Use John the Ripper with a dictionary/wordlist attack.
- Compare command-line password recovery with the NetworkWalks password-cracking lab.
- Document commands, results, and evidence in a reproducible way.

---

## 2. Tools Used

| Tool | Purpose |
|---|---|
| Kali Linux | Security testing environment |
| `pdf2john` | Extract PDF password hashes in John-compatible format |
| John the Ripper (`john`) | Dictionary-based password recovery |
| `rockyou.txt` | Wordlist used for the lab |
| NetworkWalks Hash Calculator | Extract PDF hashes through the web-based lab |
| NetworkWalks Password Cracker | Dictionary attack demonstration |

---

## 3. Lab Workflow

```text
Password-Protected PDF
        │
        ▼
   pdf2john
        │
        ▼
   PDF Hash File
        │
        ▼
John the Ripper + rockyou.txt
        │
        ▼
 Password Recovered
        │
        ▼
Verify / Document Result
```

The NetworkWalks tool demonstrates the same general workflow through a browser:

```text
PDF Upload
    │
    ▼
Local PDF Hash Extraction
    │
    ▼
Copy PDF Hash
    │
    ▼
Dictionary Attack
    │
    ▼
Password Match
```

---

## 4. Command-Line Implementation

### PDF 1

```bash
pdf2john My-Locked-PDF1.pdf > hash.txt
cat hash.txt
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

The attack completed successfully and John the Ripper reported a password match for `My-Locked-PDF1.pdf`.

### PDF 2

```bash
pdf2john My-Locked-PDF2.pdf > hash2.txt
cat hash2.txt
john --wordlist=/usr/share/wordlists/rockyou.txt hash2.txt
```

The attack completed successfully and John the Ripper reported a password match for `My-Locked-PDF2.pdf`.

### PDF 3

```bash
pdf2john My-Locked-PDF3.pdf > hash3.txt
cat hash3.txt
john --wordlist=/usr/share/wordlists/rockyou.txt hash3.txt
```

The attack completed successfully and John the Ripper reported a password match for `My-Locked-PDF3.pdf`.

---

## 5. Results

| Target | Hash extraction | Dictionary attack | Result |
|---|---:|---:|---|
| `My-Locked-PDF1.pdf` | Successful | Successful | Password recovered |
| `My-Locked-PDF2.pdf` | Successful | Successful | Password recovered |
| `My-Locked-PDF3.pdf` | Successful | Successful | Password recovered |

The command output showed successful completion for all three provided PDFs.

**Note:** Recovered passwords are intentionally not reproduced in this public README. The screenshots supplied as lab evidence contain the original lab results.

---

## 6. NetworkWalks Tool Demonstration

The NetworkWalks Hash Calculator was used to upload each password-protected PDF and extract a `pdf2john`/Hashcat-compatible PDF hash.

The accompanying Password Cracker lab then demonstrated a dictionary attack against the extracted hash. The interface displayed:

1. Extracted PDF hash
2. Active built-in wordlist
3. Password-attempt progress
4. Successful password match
5. Recovered password

The screenshots in this repository provide visual evidence of the workflow.

---

## 7. Evidence

Recommended repository structure:

```text
week-3-password-cracking/
├── README.md
├── Week3_Project_Report.docx
├── screenshots/
│   ├── My-Locked-PDF1-Hash-value.png
│   ├── My-Locked-PDF1-password.png
│   ├── My-Locked-PDF2-Hash-value.png
│   ├── My-Locked-PDF2-Password.png
│   ├── My-Locked-PDF3-hash-value.png
│   └── My-Locked-PDF3-password.png
└── commands/
    └── john-commands.txt
```

Do **not** commit unrelated personal files, real-world password hashes, private credentials, or passwords from systems you do not own or have authorization to test.

---

## 8. Key Learning

This exercise demonstrated the relationship between:

- password-protected files,
- password-derived verification data,
- hash extraction,
- dictionary wordlists,
- password-recovery tools, and
- the importance of password complexity.

A successful dictionary attack does not mean that the cryptographic protection itself was mathematically "broken." It means that a candidate password from the tested wordlist matched the password required by the protected PDF.

---

## 9. Security Takeaway

The practical lesson is that password strength matters. A password that appears sufficient to a user may still be recoverable quickly when it is predictable or present in a commonly used wordlist.

For defensive use:

- Prefer long, unique passwords/passphrases.
- Avoid common passwords and predictable patterns.
- Use a password manager for unique credentials.
- Protect sensitive documents with strong, unique passwords.
- Perform password-recovery testing only with explicit authorization.

---

## 10. Training Reference

The official Week 3 project document identifies the two mandatory project modules as **Password Cracking with JTR** and **Password Cracking with NW Tools**, and states that both essential modules must be completed. fileciteturn0file0L7-L16

The same document lists the Week 3 submission deadline as **2300H, Friday 28-August-2026**. fileciteturn0file0L19-L23

---

## Disclaimer

This repository is for cybersecurity education and authorized lab practice only. Do not use password-recovery techniques against files, accounts, systems, or data without explicit permission.
