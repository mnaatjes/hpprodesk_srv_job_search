# Email Parser Service: Credential and Permission Checklist

This document serves as a checklist to confirm the secure setup of credentials and permissions required for the Email Parser Service. **It does NOT store sensitive credentials directly.** Instead, it helps you track that these credentials have been generated and securely stored in their appropriate locations.

---

## 1. Gmail Account Information (Dedicated for Job Alerts)

*   **Email Address:** `job.michael.naatjes@gmail.com`
*   **Password:** Web234egs!
*   **Security-Key:** `8436`
*   **App Name:** `Job Alert Parser`
*   **App Password:** `obof gjwy myum fdnw`
*   **Backup:** `michael.naatjes87@gmail.com`
*   **Purpose:** Dedicated account for receiving automated job alert emails.

---

## 2. Gmail Security & Access Confirmation

Ensure these steps have been completed for the `job.michael.naatjes@gmail.com` account.

*   **2-Factor Authentication (2FA) Status:**
    *   `[x] Enabled` (Required for App Passwords)
*   **App Password Generation:**
    *   `[x] Generated` (A unique 16-digit password for service access)
*   **App Password Storage Location:**
    *   `[x] (User to fill in: e.g., personal password manager, encrypted file, Docker environment variable, .env file for local development)`

---

## 3. n8n Webhook Information

This webhook will be the secure endpoint your Python parser service sends data to.

*   **`n8n` Webhook URL Generated:**
    *   `[ ] Yes` (Obtained from your `n8n` workflow)
*   **`n8n` Webhook URL Storage Location:**
    *   `[ ] (User to fill in: e.g., personal password manager, encrypted file, Docker environment variable, .env file for local development)`

---

## 4. Other Credentials / API Keys (If Applicable)

*(Add any other credentials here as the project evolves, such as Google Sheets API keys, Wekan API tokens, etc.)*

*   **Credential Name:** `[ ] (User to fill in)`
*   **Status:** `[ ] Generated/Enabled`
*   **Storage Location:** `[ ] (User to fill in)`
