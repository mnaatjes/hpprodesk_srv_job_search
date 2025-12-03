# Workflow Example: Creating a New WordPress Landing Page

This document outlines a detailed workflow for a common WordPress task: creating a new landing page for a marketing campaign. You can use this as a guide to practice in a test WordPress environment.

**Scenario:** A sales manager asks you to create a new, simple landing page to promote a "Limited-Time 10% Off Roofing Special." The page needs to have text, an image, and a contact form for lead capture.

---

### Phase 1: Requirements & Asset Gathering

1.  **Clarify the Goal:** Confirm the purpose of the page with the manager. Who is it for? What is the single most important action you want a visitor to take? (Answer: Fill out the form).
2.  **Gather Content:**
    *   **Headline:** "Limited-Time Offer: Get 10% Off Your New Roof!"
    *   **Body Text:** Get the promotional text, explaining the terms and benefits.
    *   **Call to Action (CTA):** "Fill out the form below to claim your free inspection and lock in your discount!"
    *   **Image:** Get the approved promotional image or a relevant stock photo.
    *   **Form Fields:** What information do they need to capture? (e.g., Name, Email, Phone, Address).
    *   **Recipient Email:** Which email address should receive the lead notifications? (e.g., `sales@whitepinereno.com`).

### Phase 2: Page Creation in WordPress

1.  **Log In:** Access the WordPress admin dashboard (usually at `yourwebsite.com/wp-admin`).
2.  **Navigate to Pages:** In the left-hand menu, click on **Pages** -> **Add New**.
3.  **Set the Title:** In the main content area, add the page title: "10% Off Roofing Special".
4.  **Add Content Blocks:** Use the WordPress block editor (Gutenberg) to build the page:
    *   Click the `+` icon to add a new block.
    *   Select the **Heading** block for your headline.
    *   Select the **Paragraph** block for the body text and CTA.
    *   Select the **Image** block to upload and insert the promotional image.
5.  **Check the URL/Slug:** On the right-hand sidebar under "Summary," check the URL. By default, it will be `yourwebsite.com/10-off-roofing-special`. You can edit this if needed.

### Phase 3: Form Integration

1.  **Add Form Block:**
    *   Click the `+` icon again and search for your forms plugin block (e.g., **WPForms**, **Contact Form 7**, or another block).
    *   Select the block to add it to the page.
2.  **Configure the Form:**
    *   If creating a new form, you'll be prompted to add fields. Drag and drop the required fields (Name, Email, Phone, Address) into the form builder.
    *   Go to the form's **Settings** -> **Notifications** tab.
    *   In the "Send To Email Address" field, enter the sales team's recipient email.
    *   Customize the "Email Subject Line" to something clear, like "New Lead from 10% Off Roofing Page".
    *   Save the form.
3.  **Embed the Form:** Select the newly created form from the dropdown in the form block on your page.

### Phase 4: Styling and Review (Using CSS)

1.  **Problem:** Let's say the sales manager wants the headline to be a specific color (e.g., the company's signature blue, `#003366`) that isn't a default option.
2.  **Find the Element's Selector:**
    *   Preview the draft page in a new tab.
    *   Right-click on the headline and select **"Inspect"**.
    *   In the developer tools, you'll see the HTML. The headline is likely an `<h1>` tag. It might have a specific class like `.wp-block-heading`.
3.  **Add Custom CSS:**
    *   Go back to your WordPress admin dashboard.
    *   In the left-hand menu, navigate to **Appearance** -> **Customize**.
    *   In the Customizer menu, find and click on **"Additional CSS"**.
    *   Enter the following CSS rule:
        ```css
        h1.wp-block-heading {
          color: #003366;
        }
        ```
    *   Click the **"Publish"** button at the top.

### Phase 5: Final Review and Publish

1.  **Preview:** On the page editor, click the **Preview** button and view the page on both desktop and mobile layouts to ensure it looks good everywhere.
2.  **Test the Form:** Fill out the contact form yourself with test data. Confirm that the sales team receives the email notification with the correct subject line and information.
3.  **Publish:** Once everything is approved and tested, go back to the page editor and click the blue **"Publish"** button.
4.  **Confirm Live Page:** Navigate to the live URL to do one final check.
