# Target Company Data Schema

This document defines the data points (attributes) to collect for each target company in our outreach list. This schema will be used to structure our "Opportunities" database in Notion.

---

## Data Point Categories

To ensure an efficient research process, we will categorize attributes by their importance.

### Essential Data Points (The "Must-Haves")

These are the core pieces of information we need for every single company on our list to make the strategy work.

*   **Company Name:** The official name of the company.
*   **Website:** A direct link to their homepage.
*   **ICP Category:** A tag to identify which list they belong to (`Hospitality Tech` or `Conservative Org`).
*   **One-Liner:** A single sentence describing what the company does.
*   **Tech Stack:** A list of keywords confirming they are a fit (e.g., `PHP`, `Laravel`, `Docker`, `AWS`).
*   **Primary Contact:** The name, title, and LinkedIn URL of the best person to contact (e.g., CTO, VP of Engineering, Founder).
*   **Contact Email:** The email address for the Primary Contact.
*   **Status:** The current stage in our outreach pipeline (e.g., `Research`, `Outreach Sent`, `In Conversation`).

### High-Value Data Points (The "Should-Haves")

These attributes require a bit more research but provide the fuel for personalization and prioritization, dramatically increasing the effectiveness of our outreach.

*   **The "Hook" / Personalization Angle:** This is the **most critical field for getting replies**. It's a 1-2 sentence, custom note for each company that will go into your email.
    *   *Example for Hospitality Tech:* "As a former chef, I was impressed by how your new inventory feature solves the end-of-month waste calculation problem."
    *   *Example for Conservative Org:* "As a Hillsdale alumnus, I've followed your organization's work on [specific policy] for years."
*   **Growth Signals:** Is the company in a position to hire? Look for these signs:
    *   Are they currently hiring engineers? (Check their careers page).
    *   Have they received recent funding? (A quick search on Crunchbase or TechCrunch).
    *   Have they had a recent product launch or positive press?
*   **Secondary Contact / Referrer:** Find one other person at the company, like a Senior Developer. Mentioning their work or asking for a referral shows you've done your homework.

### Lower Priority / Less Useful Data

We will not spend significant time on these points, as they have a low return on investment for the time required to find them.

*   **`relevant job title information`:** For our direct outreach strategy, we assume a job may *not* be posted. An open role is a great "Growth Signal," but we will not limit our search to only these companies.
*   **`hiring platforms` & `frequency of postings`:** This information is very difficult to find without expensive, specialized software. The time is better spent personalizing the "hook" for another target company.

---

## The Final Notion Database Schema

This is the list of properties to configure for each company in the Notion database:

1.  **Company Name** (Text)
2.  **Website** (URL)
3.  **ICP Category** (Select: `Hospitality Tech`, `Conservative Org`)
4.  **Status** (Select: `Research`, `Outreach Sent`, etc.)
5.  **One-Liner** (Text)
6.  **Tech Stack** (Multi-Select: `PHP`, `Docker`, etc.)
7.  **Growth Signals** (Text Area for notes)
8.  **The Hook** (Text Area for your custom sentence)
9.  **Primary Contact** (Text)
10. **Contact LinkedIn** (URL)
11. **Contact Email** (Email)
12. **Next Follow-up Date** (Date)
