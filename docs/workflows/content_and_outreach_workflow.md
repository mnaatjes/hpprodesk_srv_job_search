# Content & Outreach: Execution Workflow

This document provides the step-by-step workflow for executing your inbound content strategy and your outbound outreach campaigns.

---

## 1. The Execution Workflow Diagram

This diagram shows the two parallel "engines" of your job search: Inbound (attracting leads with content) and Outbound (contacting targets directly). Both are designed to feed your pipeline with opportunities.

```mermaid
graph TD
    subgraph "Inbound Engine (Content Marketing)"
        A[Write Article Based on a Project Case Study] --> B[Publish on a Primary Platform (e.g., Medium)];
        B --> C[Distribute Article Link on Socials (LinkedIn, Twitter, etc.)];
        C --> D{Inbound Leads & Engagement};
    end

    subgraph "Outbound Engine (Direct Outreach)"
        E[Select Target from Notion Board] --> F[Personalize Email Template with Custom Hook];
        F --> G[Send Email & Track in Notion];
        G --> H{Replies & Conversations};
    end

    D --> I([New Opportunities & Interviews]);
    H --> I;
```

---

## 2. One-Time Account Setup Checklist

Before you begin, make sure you have accounts on the necessary platforms.

- [ ] Create a free account on [Medium](https://medium.com/).
- [ ] Create a free account on [dev.to](https://dev.to/).
- [ ] Create a free account on [Hashnode](https://hashnode.com/).
- [ ] Ensure your [LinkedIn](https://linkedin.com/) profile is complete and up-to-date.
- [ ] **Note:** [Close.com](https://close.com/)'s blog is a resource for learning sales strategy; it is not a platform for posting content.

---

## 3. The Inbound Content Workflow (Repeatable Checklist)

Follow this checklist each time you publish a new article.

### Pre-Publish
- [ ] Finalize the draft of your article in a text editor.
- [ ] Choose the best primary platform (Medium, dev.to, or Hashnode) for this specific article.
- [ ] **Crucially:** Add at least 2-3 links within the article that point back to the full case study on your GitHub.io site.
- [ ] Add a clear Call to Action (CTA) at the end of the article (e.g., "To see the full project, visit my portfolio here...").

### Publish & Distribute
- [ ] Publish the article on your chosen platform.
- [ ] Post a link to the article on your LinkedIn feed with a brief summary and relevant hashtags (e.g., `#PHP`, `#DevOps`, `#WebDev`).
- [ ] Post a link on Twitter/X with relevant hashtags.
- [ ] If appropriate, share a link in relevant Reddit communities (e.g., `r/php`, `r/laravel`, `r/devops`). Be sure to follow the community's rules on self-promotion.

### Post-Publish
- [ ] Add the link to your new article to your `outreach_campaign_worksheet.md`. This can be used as a value-add in follow-up emails.
- [ ] After one week, check the analytics (views, comments, likes) and make a note of what topics seem to resonate most with people.

---

## 4. The Outbound Campaign Workflow (Repeatable Checklist)

Follow this checklist for your weekly or bi-weekly outreach sessions. This workflow is designed to be used with your **Notion Command Center** and your **Outreach Campaign Worksheet**.

### On Your "Outreach Day"
- [ ] Open your `Opportunities` database in Notion.
- [ ] Open your `outreach_campaign_worksheet.md` file.
- [ ] Focus only on the companies in your "Research" column.
- [ ] For each company:
    - [ ] **Step 1: Personalize.** Read the pre-filled template in your worksheet. Spend 3-5 minutes on the company's website to find the detail for your `[Custom Hook]`.
    - [ ] **Step 2: Send.** Copy the completed, personalized email and send it from your professional email address.
    - [ ] **Step 3: Update Status.** In Notion, drag the company's card from the `Research` column to the `Outreach Sent` column.
    - [ ] **Step 4: Set Follow-up.** Set the `Next Follow-up Date` property on the card to 3-5 business days from today. Your Calendar view will now automatically track this.

### On Your "Follow-Up Day"
- [ ] Open the "Calendar View" of your `Opportunities` database. This is your to-do list.
- [ ] For each company that appears on today's date:
    - [ ] Check your email for a reply.
    - [ ] **If no reply:** Send your `F1 - Simple Follow-Up` template. Then, set a *new* `Next Follow-up Date` for 4-5 days in the future.
    - [ ] **If you got a reply:** Drag their card to the `In Conversation` column and add a note about the next action. Clear the `Next Follow-up Date`.
