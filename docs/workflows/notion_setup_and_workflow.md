# Notion Command Center: Setup & Workflow

This document provides a step-by-step guide for setting up and using your Notion workspace as a central command center for your job search.

---

## Part 1: One-Time Setup Checklist

Follow these steps to build your workspace from scratch.

- [ ] **1. Create Your HQ Page:**
    - [ ] In Notion, create a new, empty page. Title it `Job Search HQ`.

- [ ] **2. Create the "Opportunities" Database:**
    - [ ] On the `Job Search HQ` page, type `/database` and select "Database - Full page".
    - [ ] Name the new database `Opportunities`.
    - [ ] **Configure the properties (columns)** to match our schema. Delete any default properties and add the following:
        - `Company Name` (Title)
        - `Rating` (Select)
        - `Website` (URL)
        - `ICP Category` (Select - with options `Hospitality Tech` and `Conservative Org`)
        - `Status` (Select - with options `Research`, `Outreach Sent`, `In Conversation`, `Proposal Sent`, `Won`, `Lost`, `Archived`)
        - `One-Liner` (Text)
        - `Tech Stack` (Multi-select)
        - `Growth Signals` (Text)
        - `The Hook` (Text)
        - `Primary Contact` (Text)
        - `Contact LinkedIn` (URL)
        - `Contact Email` (Email)
        - `Next Follow-up Date` (Date)

- [ ] **3. Set Up the Board View:**
    - [ ] By default, you should be in a Table view. Click the `+` next to "Table" to add a new view.
    - [ ] Select "Board" as the view type.
    - [ ] In the Board settings, set "Group by" to the `Status` property. This creates your visual pipeline.
    - [ ] Drag the columns to match the logical flow: `Research` -> `Outreach Sent` -> `In Conversation` -> etc.

- [ ] **4. Set Up the Calendar View:**
    - [ ] Click the `+` again to add another new view.
    - [ ] Select "Calendar" as the view type.
    *   In the Calendar settings, set "Show calendar by" to the `Next Follow-up Date` property. This is now your automatic follow-up dashboard.

- [ ] **5. Create the "Campaign Kit" Page:**
    - [ ] Go back to your main `Job Search HQ` page.
    - [ ] Type `/page` and create a new page. Title it `Campaign Kit`.
    - [ ] On this page, you will paste the email templates we draft.

- [ ] **6. Create a "New Target" Template (Optional but Recommended):**
    - [ ] In your `Opportunities` database, click the down-arrow next to the blue "New" button.
    - [ ] Click "+ New template".
    - [ ] Title the template `New Target Checklist`.
    - [ ] In the body of the template, create a checklist:
        - `[ ]` Find company website and one-liner.
        - `[ ]` Confirm Remote Policy.
        - `[ ]` Identify Tech Stack.
        - `[ ]` Identify Primary Contact & LinkedIn URL.
        - `[ ]` Research and write a custom "Hook".
    - [ ] Now, whenever you add a new company, you can apply this template to get a fresh checklist.

---

## Part 2: Daily & Weekly Workflow

This is a repeatable process for using your Notion Command Center.

### The "Add a New Target" Workflow

- [ ] In your `Opportunities` database, go to the "Research" column and click `+ New`.
- [ ] Apply the `New Target Checklist` template you created.
- [ ] As you research a company, fill in the properties at the top of the page and check off the items on your list.

### The "Outreach Day" Workflow (e.g., on a Monday)

- [ ] Open your `Campaign Kit` page in one tab and your `Opportunities` database in another.
- [ ] For each company in your "Research" column that is ready for outreach:
    - [ ] Copy the appropriate email template (`T1` or `T2`).
    - [ ] Paste it into a new email draft.
    - [ ] Copy the `Primary Contact`, `Company Name`, and your custom `Hook` from Notion into the email.
    - [ ] Send the email.
    - [ ] **Crucially:** Drag the company's card from the `Research` column to the `Outreach Sent` column.
    - [ ] Set the `Next Follow-up Date` property to 3-5 days from today.

### The "Follow-Up Day" Workflow (e.g., on a Thursday)

- [ ] Open the "Calendar View" of your `Opportunities` database. This is your to-do list.
- [ ] For every company card that appears on today's date:
    - [ ] Check your email for a reply from them.
    - [ ] **If no reply:** Send your `F1 - Simple Follow-Up` template. Then, click on the card and set a *new* `Next Follow-up Date` for 4-5 days in the future.
    - [ ] **If you got a reply:** Drag their card to the `In Conversation` column. Add a note to the card about the next action (e.g., "Replied, need to schedule a call"). Clear the `Next Follow-up Date` for now.