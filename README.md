# 🏦 Vulnerable Bank Security Assessment

**Author:** Joeassessment1  
**Date:** February 2026  
**Role:** QA Engineer Assessment - CredPal  
**Repository:** Public Portfolio

---

## 📋 **Overview**

This repository contains my complete security assessment of the **vuln-bank** application, a deliberately vulnerable banking platform designed for security testing practice. The assessment was conducted as part of the QA Engineer hiring process for CredPal.

The application was tested for:
- 🔐 Authentication & Authorization vulnerabilities
- 💸 Money Transfer logic flaws
- 📁 File Upload & SSRF exploits
- 📃 Bill Payment vulnerabilities
- ⏱️ Rate Limiting & Session Management issues

---

## 🚨 **Executive Summary**

A total of **8 security vulnerabilities** were identified, including **5 critical** and **3 high-risk** findings. The application suffers from severe flaws that could lead to complete compromise in a production environment.

| Severity | Count |
|----------|-------|
| 🔴 Critical | 5 |
| 🟠 High | 2 |
| 🟡 Medium | 1 |
| 🟢 Low | 0 |

---

## 📊 **Findings Summary**

| # | Finding | Severity | Category |
|---|---------|----------|----------|
| 1 | Unrestricted File Upload (PHP upload allowed) | 🔴 CRITICAL | File Upload |
| 2 | SSRF via Import from URL exposing database credentials | 🔴 CRITICAL | SSRF |
| 3 | JWT Weak Secret (`secret123`) allowing token forgery | 🔴 CRITICAL | Authentication |
| 4 | Negative Money Transfer allowing arbitrary money creation | 🔴 CRITICAL | Business Logic |
| 5 | Missing Rate Limiting enabling brute force attacks | 🟠 HIGH | Rate Limiting |
| 6 | No Session Expiration (JWT tokens never expire) | 🟠 HIGH | Session Management |
| 7 | Information Disclosure (system details exposed) | 🟡 MEDIUM | Information Disclosure |
| 8 | Zero Amount Transactions accepted | 🟡 LOW | Input Validation |

---

## 📦 **Deliverables Included**

| File | Description |
|------|-------------|
| `vuln-bank-security-tests.json` | Postman collection with all test requests |
| `vuln-bank-test-report.pdf` | Detailed report with steps to reproduce, risk ratings, and screenshots |
| `screenshots/` | Folder containing evidence images for each finding |

---

## 🛠️ **How to Use This Collection**

### Prerequisites
- [Postman](https://www.postman.com/downloads/) installed
- vuln-bank application running locally (`docker-compose up --build`)

### Setup Instructions

1. **Import the collection:**
   - Open Postman
   - Click **Import** → **Upload Files**
   - Select `vuln-bank-security-tests.json`

2. **Set up environment:**
   - Create a new environment called `vuln-bank-local`
   - Add variable: `base_url` = `http://localhost:5000`
   - Add variable: `jwt_token` (will be populated automatically)

3. **Run the requests in order:**
   - Start with **Login - Get Token** to authenticate
   - Run remaining tests in any order

---

## 🔍 **Detailed Findings**

### 🔴 **Finding 1: Unrestricted File Upload**
**Endpoint:** `/upload_profile_picture`  
**Description:** The application allows upload of PHP files disguised as images.  
**Impact:** Remote code execution risk, server compromise.

### 🔴 **Finding 2: SSRF + Secrets Exposure**
**Endpoint:** `/upload_profile_picture_url`  
**Description:** The "Import from URL" feature allows fetching internal endpoints, exposing database credentials and JWT secret.  
**Impact:** Full database access, token forgery.

### 🔴 **Finding 3: JWT Weak Secret**
**Description:** JWT secret `secret123` was exposed via SSRF, allowing attackers to forge valid tokens.  
**Impact:** Privilege escalation, account takeover.

### 🔴 **Finding 4: Negative Money Transfer**
**Endpoint:** `/transfer`  
**Description:** Sending negative amounts increases balance instead of decreasing it.  
**Impact:** Unlimited money creation.

### 🟠 **Finding 5: Missing Rate Limiting**
**Endpoint:** `/login`  
**Description:** No rate limiting on login endpoint allows unlimited brute force attempts.  
**Impact:** Password guessing, account compromise.

### 🟠 **Finding 6: No Session Expiration**
**Description:** JWT tokens contain no `exp` claim and remain valid indefinitely, even after logout.  
**Impact:** Token theft leads to permanent account access.

### 🟡 **Finding 7: Information Disclosure**
**Description:** Internal files expose system details (OS, Python version).  
**Impact:** Helps attackers plan targeted exploits.

### 🟡 **Finding 8: Zero Amount Transactions**
**Description:** Transfers with amount `0` are accepted.  
**Impact:** Log clutter, potential for more complex attacks.

---

## 📸 **Screenshots**

All evidence screenshots are available in the `/screenshots` folder:

| Finding | Screenshot |
|---------|------------|
| 1 | `finding1-upload-success.png` |
| 2 | `finding2-ssrf-secret.png` |
| 3 | `finding3-jwt-forgery.png` |
| 4 | `finding4-negative-transfer.png` |
| 5 | `finding5-rate-limiting.png` |
| 6 | `finding6-no-expiration.png` |
| 7 | `finding7-info-disclosure.png` |
| 8 | `finding8-zero-amount.png` |

---

## 🧪 **Technologies Used**

- **Postman** - API testing and automation
- **Docker** - Local application setup
- **JWT.io** - Token decoding and forgery
- **Browser DevTools** - Network analysis
- **Git/GitHub** - Version control and portfolio

---

## 📝 **Notes**

- This assessment was performed on a **deliberately vulnerable** application for educational purposes
- All "secrets" exposed are fake/test credentials
- The application was run locally in an isolated Docker container
- No real data or systems were harmed 🛡️

---

## 📬 **Contact**

**Joeassessment1**  
[Your Email Address]  
[Your LinkedIn Profile URL]

---

## 📄 **License**

This project is for **portfolio and educational purposes only**. The findings demonstrate security testing methodology and should not be used against real systems.

---

## 🙏 **Acknowledgments**

- CredPal for the assessment opportunity
- Commando-X for creating the vuln-bank application
- The security testing community for knowledge sharing

---

⭐ **If you found this useful, feel free to star the repo!**