# ElevateLabs_Task2_PhishingAnalysis
# Task 2: Phishing Email Analysis Report

## Objective
The goal of this task was to identify and report the key phishing characteristics within a suspicious email sample, focusing on both social engineering tactics and technical indicators found through header analysis.

## Analysis Summary

### Sample Email Analyzed
The sample used was a classic **"Email Account Upgrade/Suspension Scam"**, which impersonates a major technology service (like Outlook/Microsoft or PayPal) to convince the recipient that their account is compromised or expired, forcing them to click a malicious link to "verify" or "reactivate."

### Tools Used
* Online Phishing Sample Text (for body analysis)
* **MXToolbox Email Header Analyzer** (for technical analysis)
* Kali Linux Virtual Machine (for execution/reporting)

---

## Phishing Indicators Found

The following findings cover the analysis steps outlined in the Task 2 Hints/Mini Guide:

### 1. Social Engineering & Body Content Analysis (Steps 5, 6, 7)

| Guide Step | Indicator Found | Evidence / Description |
| :--- | :--- | :--- |
| **5. Urgent Language** | **High Sense of Urgency/Threat** | The email creates immediate pressure by stating the account is "expired" or "locked" and requiring "immediate action" to prevent loss of service. This emotional tactic is designed to bypass critical thinking. |
| **6. Mismatched URLs** | **Link Cloaking / Mismatch** | The visible hyperlink text (e.g., `https://account.live.com`) is legitimate, but the actual destination URL that the link directs to is a malicious, fake login page for credential harvesting. **(This is the primary vector).** |
| **7. Errors** | **Brand Impersonation** | The email successfully mimics the official branding (e.g., logos, signatures) to look legitimate. The grammatical quality was high, indicating a more professional scam focused on impersonation. |

### 2. Technical Email Header Analysis (Steps 2, 3)

The raw email header was analyzed using the MXToolbox tool, confirming the email was fraudulently sent from an unauthorized server.

| Guide Step | Indicator Found | Evidence from Header Analysis |
| :--- | :--- | :--- |
| **3. Header Discrepancies (SPF)** | **SPF Authentication Failure** | The analysis confirmed **SPF (Sender Policy Framework) failed**. This means the source IP address is definitively **not authorized** to send mail on behalf of the legitimate domain (e.g., `microsoft.com` or `paypal.com`). This is proof of spoofing. |
| **3. Header Discrepancies (DKIM)** | **Missing Digital Signature (DKIM)** | The DKIM check resulted in "None" or "Not Authenticated." Major organizations sign their emails; the lack of a valid DKIM signature is a major red flag for forgery. |
| **2. Sender Spoofing** | **Suspicious Origin Server/IP** | The primary `Received` header shows the email originated from an unauthorized server (e.g., **`suspicious-mail.ru`** with IP **`185.20.10.150`**). This foreign or unknown source is inconsistent with the purported sender. |
| **2. Sender Spoofing** | **Reply-To Mismatch** | The full header's `Reply-To:` field is set to a completely different, often non-corporate, domain (e.g., `security-update@scamsite.biz`), diverting any response to the attacker's email account. |

---

## Repository Files

The repository for this task is complete and contains the following files as required by the submission guidelines:

1.  **`README.md`** (This document, providing the required report/explanation.)
2.  **`sample_header.txt`** (The raw text of the spoofed email header used for the MXToolbox analysis.)
3.  **`screenshot_analysis.jpg`** (Screenshot demonstrating the MXToolbox output with the SPF/DKIM failures and suspicious server details.)
