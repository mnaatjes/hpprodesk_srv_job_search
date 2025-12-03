# Email Parser Service: Master Plan

## 1. Overview

This document outlines the plan for creating an automated service that pulls job alert emails from a designated Gmail account, parses them to extract structured data, and uses `n8n` to create new cards on a `Wekan` board.

The service will be designed to be robust, maintainable, and isolated in its own environment.

---

## 2. Architecture

As requested, the service will be isolated in its own subdirectory and run as a dedicated container, communicating with the existing `n8n` service over the shared Docker network.

*   **Directory:** `/srv/job-search/email_parser/`
*   **Docker Environment:** The new directory will contain its own `docker-compose.yml` to define and run the Python service.
*   **Networking:** The service will be attached to the existing `jobsearch-tools` Docker network to allow it to communicate with `n8n`.
*   **Secret Management:** All sensitive data (Gmail credentials, webhook URLs) will be managed via environment variables passed into the container, not hard-coded.

---

## 3. Workflow

The process is a "pull-then-push" model, where the Python service pulls data from Gmail and pushes it to `n8n`.

1.  **Scheduled Trigger:** A Docker container running a Python application is initiated on a schedule (e.g., every 15 minutes via `cron`).
2.  **Fetch Emails:** The Python script connects to the specified Gmail account using the IMAP protocol and a secure App Password.
3.  **Parse & De-duplicate:** The script fetches all unread emails from a specific label (e.g., `job-alerts`). It parses the HTML content of each email to extract the job title, company, and job URL. It checks a local cache (e.g., a simple SQLite DB file) to see if this job URL has been processed before.
4.  **Push to n8n:** For each new, unique job, the script makes an HTTP POST request to a dedicated `n8n` Webhook URL, sending the clean, structured JSON data.
5.  **n8n Processing:** The `n8n` workflow receives the data and uses its native `Wekan` node to create a new card on the "Job Search" board in the "Inbox" list.
6.  **(Optional) Analytics Logging:** The `n8n` workflow can simultaneously send the data to a Google Sheet or database for long-term analytics.

***Workflow Alternative Note:*** *An alternative, simpler architecture would be to use the native `n8n` IMAP and Cron nodes to perform the email polling directly within an `n8n` workflow. This would eliminate the need for a separate Python service and Docker container. The current plan proceeds with the dedicated service as requested, as it provides a clean separation of concerns and allows for potentially more complex Python-based parsing logic.*

---

## 4. Todo List

### Phase 1: Service Configuration & Setup (Completed)
- [x] Create a new dedicated Gmail address for receiving job alerts (e.g., `job.michael.naatjes@gmail.com`).
- [x] Update your job search profiles (Indeed, LinkedIn, etc.) to send all job alerts to this new dedicated email address.
- [x] Create directory: `mkdir -p /srv/job-search/email_parser`
- [ ] In your Gmail account:
    - [x] Enable 2-Factor Authentication.
    - [x] Generate a 16-digit App Password for the service.
    - [x] Create a specific label/folder (e.g., `job-alerts`).
    - [x] Create filters to automatically move job alerts into it.

### Phase 2: The Parser Service (Pending)
- [ ] Create a `requirements.txt` file in `email_parser/` with necessary Python libraries:
    *   `imap-tools`
    *   `beautifulsoup4`
    *   `requests`
    *   `python-dotenv` (for managing environment variables)
- [ ] Develop the core script `email_parser/parser.py`.
    - [ ] Implement IMAP connection using environment variables for credentials.
    - [ ] Implement logic to fetch unread emails from the specific label.
    - [ ] Implement HTML parsing to extract job data.
    - [ ] Implement a de-duplication mechanism (e.g., using a local SQLite file to store processed URLs).
    - [ ] Implement the HTTP POST request to the (future) `n8n` webhook URL.
    - [ ] Implement logic to mark emails as "read" or move them after processing.
- [ ] Create `email_parser/Dockerfile` to build a container for the Python script.
- [ ] Create a `crontab` file to schedule the script execution. The Dockerfile will copy this in and set up `cron`.

### Phase 3: The n8n Workflow (Pending)
- [ ] In the `n8n` UI, create a new workflow.
- [ ] Add a **Webhook node** as the trigger. Copy its URL.
- [ ] Connect a **Wekan node** and configure it to create a card with the data received by the webhook.
- [ ] (Optional) Connect a **Google Sheets node** to log the job data to a spreadsheet.
- [ ] Activate the workflow.

### Phase 4: Dockerization & Deployment (Pending)
- [ ] Create `email_parser/docker-compose.yml`.
    - [ ] Define the `email-parser` service, building from the Dockerfile.
    - [ ] Attach the service to the external `jobsearch-tools` network.
- [ ] Create a `.env` file in `email_parser/` to store secrets:
    *   `GMAIL_USER`
    *   `GMAIL_APP_PASSWORD`
    *   `N8N_WEBHOOK_URL`
- [ ] Launch the service and test the deployment.

### Phase 5: End-to-End Testing (Pending)
- [ ] Manually trigger the service or wait for the cron schedule.
- [ ] Verify that new emails result in new, de-duplicated cards on the Wekan board.
- [ ] Verify data is appearing correctly in the analytics store (if configured).
- [ ] Review service logs for any errors.

---

## 5. Appendix

### A.1 - Known Issues
*(No issues logged yet.)*

### A.2 - Future Improvements
*   Add support for parsing job data from email attachments (e.g., `.ics` files).
*   Improve the de-duplication cache to use a more robust database.
*   Add error notification (e.g., send a Discord/Slack message from `n8n` if the workflow fails).
