# Wekan & n8n Setup Checklist

This is a step-by-step guide to resolve system issues and get your new services running.

---

### Phase 1: System Maintenance (Required)

This phase resolves the Docker version incompatibility on your server.

- [x] **1. Identify Running Services:**
  - [x] Run `docker ps` to see which containers are currently active.

- [x] **2. Gracefully Stop Critical Services (Optional but Recommended):**
  - [x] If you have critical services running, stop them gracefully before proceeding (e.g., `docker compose down` in their respective directories).

- [x] **3. Update Your System's Package List:**
  - [x] Run the following command:
    ```bash
    sudo apt-get update
    ```

- [x] **4. Upgrade Docker Components:**
  - [x] Run the following command to upgrade the Docker client and related packages:
    ```bash
    sudo apt-get install --only-upgrade docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
    ```

- [x] **5. Restart Services:**
  - [x] Restart any services you manually stopped in step 2.

---

### Phase 2: Deploy Your Services

Once Phase 1 is complete, you can start your new tools.

- [x] **1. Create Shared Docker Network (If not already done):**
  - [x] Run the following command:
    ```bash
    docker network create jobsearch-tools
    ```

- [x] **2. Start the Wekan Service:**
  - [x] Run the following command. This will pull the correct image and recreate the containers with the fixed configuration.
    ```bash
    cd /srv/dev/job-search/wekan && docker compose up -d --force-recreate
    ```

- [x] **3. Start the n8n Service:**
  - [x] Run the following command:
    ```bash
    cd /srv/dev/job-search/n8n && docker compose up -d
    ```

---

### Phase 3: Verify Installation

- [x] **1. Access Wekan:**
  - [x] Open your web browser and navigate to `http://<your-server-ip>:9999`.
  - [x] Create your initial administrator account.

- [x] **2. Access n8n:**
  - [x] Open your web browser and navigate to `http://<your-server-ip>:5678`.
  - [x] Create your initial owner account.

---

### Phase 4: Future Improvements (Optional)

- [ ] **1. Harden n8n Configuration:**
  - [ ] Consider updating the `/srv/dev/job-search/n8n/docker-compose.yml` file to include the recommended environment variables (like `N8N_ENCRYPTION_KEY`) to improve security and prevent future deprecation warnings.

---

### Phase 5: Automated Job Aggregation (ABANDONED)

This phase sets up `jobfunnel`, a self-hosted service to automatically scrape and collect job postings from various boards. **This effort was abandoned due to the installed version of `jobfunnel` (v3.0.0) being non-functional.** See the appendix for a full troubleshooting summary.

- [x] **1. Create the `jobfunnel` Directory:**
  - [x] Create a new directory for the service:
    ```bash
    mkdir -p /srv/dev/job-search/jobfunnel/output
    ```

- [x] **2. Create the `config.yaml` File:**
  - [x] Create a file named `/srv/dev/job-search/jobfunnel/config.yaml`.

- [x] **3. Create the `Dockerfile`:**
  - [x] Create a file named `/srv/dev/job-search/jobfunnel/Dockerfile`.

- [x] **4. Create the `docker-compose.yml` File:**
  - [x] Create a file named `/srv/dev/job-search/jobfunnel/docker-compose.yml`.

- [ ] **5. Run the Job Scraper:**
  - [ ] Navigate to the directory and run the service.

- [ ] **6. Review the Results:**
  - [ ] Check the output file at `/srv/dev/job-search/jobfunnel/output/jobs.csv`.

---

### Phase 6: Lead Generation & Prospecting

This phase involves using a professional web service to find companies and key contacts, which is more efficient than attempting to build a custom scraper.

- [ ] **1. Create an `Apollo.io` Account:**
  - [ ] Go to the [Apollo.io](https://www.apollo.io/) website and sign up for their free tier.

- [ ] **2. Install the Chrome Extension (Recommended):**
  - [ ] Install the Apollo Chrome extension to get contact information directly from LinkedIn profiles.

- [ ] **3. Configure Search Filters:**
  - [ ] Inside Apollo, use the "Search" feature to filter for companies that match your Ideal Client Profile (e.g., by industry, employee count, technologies used).

- [ ] **4. Build Prospecting Lists:**
  - [ ] Create lists of target companies.
  - [ ] For each company, search for relevant contacts (CTOs, VPs of Engineering, Hiring Managers) and add them to your lists.
  - [ ] Use your free monthly credits to reveal their email addresses.

- [ ] **5. Integrate with Your Workflow:**
  - [ ] Manually add the high-potential leads you find in Apollo to your Wekan board to track your outreach efforts.
  - [ ] (Optional Advanced) Use `n8n` to connect to the Apollo API to automate parts of this process.

---
---

## Appendix A: Jobfunnel (v3.0.0) Troubleshooting Summary

### Objective
The goal was to set up the `jobfunnel` automated job scraping tool as outlined in Phase 5.

### Conclusion
After extensive troubleshooting, it was determined that the `jobfunnel` package (version 3.0.0, by PaulMcInnis) is **non-functional**. The scrapers for all supported providers (`INDEED`, `MONSTER`, `GLASSDOOR`) are broken, likely due to changes in the HTML structure of the target websites. It is recommended to abandon this tool and explore alternatives.

### Additional Conclusion from Repository Review:
Further investigation into the `JobFunnel` GitHub repository confirms the project's effectively abandoned status. The last significant commit was over a year ago, indicating a lack of active maintenance. While a fix for the Indeed scraper (addressing CAPTCHA issues) was merged, it appears to be either insufficient or quickly outdated due to continuous website changes. This confirms that the scrapers are highly brittle and would require constant, dedicated maintenance that the project currently lacks, making it an unreliable solution for ongoing job aggregation.

### Troubleshooting Steps Attempted
The setup process involved a lengthy debugging cycle to resolve a series of cascading errors.

1.  **`executable file not found in $PATH`**:
    *   **Problem**: The `jobfunnel` executable was not in the container's default path.
    *   **Solution**: Identified the correct executable name (`funnel`) and its full path (`/usr/local/bin/funnel`).

2.  **`invalid choice: 'search'`**:
    *   **Problem**: The `search` command was not valid in this version.
    *   **Solution**: Discovered the correct command was `load`.

3.  **`the following arguments are required: -s`**:
    *   **Problem**: The `load` command required a settings file argument.
    *   **Solution**: Added the `-s config.yaml` argument to the `CMD` in the Dockerfile.

4.  **`Invalid Config settings yaml` (Multiple Occurrences)**:
    *   **Problem**: The `config.yaml` file did not match the strict schema enforced by the `Cerberus` validation library used in `jobfunnel v3.0.0`.
    *   **Solution**: This required a deep dive to reverse-engineer the correct schema.
        *   Discovered the list of supported `providers` (`INDEED`, `MONSTER`, `GLASSDOOR`) by inspecting the package's internal `enums.py` file.
        *   Identified all required top-level fields (`master_csv_file`, `block_list_file`, etc.).
        *   Corrected the structure of the `search` dictionary, renaming keys (`provinces` -> `province_or_state`) and adding required fields (`locale`).
        *   Added the required `delay` section.
        *   Experimented with different values for `city` and `province_or_state` to satisfy validation rules (e.g., must not be empty).

5.  **`ValueError: Unable to identify number of pages of results` (INDEED)**:
    *   **Problem**: After fixing all configuration issues, the Indeed scraper failed to parse the search results page.
    *   **Solution**: Numerous attempts were made to simplify the query, including reducing keywords and testing various location and remoteness settings. The error persisted even with the most basic possible query (`keyword: PHP`, `provider: INDEED`, `location: New York, NY`).

6.  **`AttributeError: 'NoneType' object has no attribute 'text'` (MONSTER)**:
    *   **Problem**: Switched the provider to `MONSTER`, which also failed. The error indicated it could not find a required HTML element on the Monster search results page.

This exhaustive process confirmed that the scrapers themselves are broken and cannot be fixed with configuration changes alone.

---

## Appendix B: Alternative Job Scraper Options

Since JobFunnel has proven non-functional, here are alternative options for job scraping, ranging from ready-to-use open-source projects to powerful frameworks for building custom solutions.

### 1. Other Open-Source Job Scrapers

These projects are direct alternatives to JobFunnel. Always check their GitHub repositories for active maintenance and supported job boards before committing.

*   **`Job-scraper` by h-chao:** A popular and generally well-documented open-source project designed for scraping various job boards. Verify its current functionality and supported sites.
*   **Specialized LinkedIn Scrapers:** Projects like `linkedin-jobs-scraper` focus specifically on LinkedIn. While effective, LinkedIn actively works against scrapers, making these tools potentially brittle and requiring frequent updates.

### 2. DIY with Scraping Frameworks (Requires Coding)

This approach offers the most control and long-term reliability, as you can adapt your scraper to website changes.

*   **Scrapy (Python Framework):** A powerful, asynchronous Python framework for large-scale web scraping. It's highly efficient, robust, and has a strong community. Ideal for building complex and maintainable scraping solutions.
*   **Beautiful Soup (Python Library):** Excellent for parsing HTML and XML documents. It's simpler to learn than Scrapy and pairs well with HTTP libraries like `requests` for fetching web pages. Best for smaller, targeted scraping tasks.
*   **Selenium / Playwright (Browser Automation):** These tools automate a web browser (e.g., Chrome, Firefox). They are slower than direct HTTP requests but excel at scraping dynamic, JavaScript-heavy websites and handling interactions like clicks, form submissions, and waiting for content to load. Can often bypass simple bot detection.

### 3. Commercial & Low-Code Tools

These services abstract away much of the technical complexity, often for a fee.

*   **Apollo.io / Hunter.io:** Primarily lead-generation and email-finding platforms. They are highly reliable for gathering company and contact data but are not designed for aggregating job postings from various boards.
*   **Apify / Octoparse (Scraping-as-a-Service):** Platforms that provide pre-built scrapers for many websites, handling maintenance, proxy rotation, and CAPTCHA solving. They typically offer free tiers with paid plans for larger volumes.