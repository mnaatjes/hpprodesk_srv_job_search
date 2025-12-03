# Workflow Example: Onboarding a New Sales Rep in the CRM

This document outlines a detailed workflow for a common administrative task in a sales CRM: setting up a new user account. You can use this as a mental model for how you would approach system administration.

**Scenario:** A new sales representative, "Jane Doe," has joined the team. You need to create her account in the company's CRM (e.g., MarketSharp, LEAP), assign the correct permissions, and ensure she can log in successfully.

---

### Phase 1: Information Gathering

1.  **Confirm User Details:** Get the official user information from HR or the hiring manager. You will need:
    *   **Full Name:** Jane Doe
    *   **Email Address:** `jane.doe@whitepinereno.com`
    *   **Job Title:** Sales Representative
    *   **Team/Manager:** Reports to the Sales Manager.
    *   **Start Date:** The user's first day.
    *   **Sales Territory (if applicable):** e.g., "Kalamazoo County".

### Phase 2: User Account Creation

1.  **Log In as Administrator:** Access the CRM with your administrative credentials.
2.  **Navigate to User Management:** Find the administrative section for managing users. This is typically labeled **"Settings," "Admin," "Setup,"** or **"Staff Management."**
3.  **Create New User:** Click the **"Add New User," "Create User,"** or similar button.
4.  **Enter Basic Information:** Fill in the fields with the information gathered in Phase 1 (Name, Email, Title).
5.  **Assign a Role/Profile:**
    *   Look for a dropdown labeled **"Role," "Profile,"** or **"Permission Set."**
    *   Select the pre-defined profile for **"Sales Representative."** This is crucial as it will determine what the user can see and do. Avoid assigning "Administrator" privileges.
    *   *If a "Sales Representative" role doesn't exist, you would need to create one, carefully configuring its permissions (e.g., can view/edit own leads, cannot delete records, cannot export data, cannot access system settings).*

### Phase 3: System & Territory Configuration

1.  **Assign to a Territory:** If the CRM uses sales territories, navigate to the territory settings and assign Jane Doe to the "Kalamazoo County" territory. This will ensure she automatically gets new leads from that area.
2.  **Check Lead Assignment Rules:**
    *   Navigate to the lead assignment or routing rules section.
    *   If the company uses a "round-robin" system for assigning new web leads, ensure Jane Doe is added to the active rotation.
3.  **Configure Call/Email Settings:** If the CRM has built-in calling or emailing, you may need to assign a phone number or configure her email signature.

### Phase 4: Finalization and Communication

1.  **Set Initial Password:**
    *   **Option A (Best):** Trigger the system's "Welcome Email." This will send an email to `jane.doe@whitepinereno.com` with a link to set her own password.
    *   **Option B (Manual):** If a welcome email isn't an option, set a strong, temporary password and communicate it to her securely (e.g., via a password manager, or in person). Instruct her to change it immediately upon her first login.
2.  **Save the User Record:** Click "Save" or "Create" to finalize the account.
3.  **Provide Login Instructions:** Send an email or message to Jane Doe (or her manager) with the CRM login URL and basic instructions for her first day.

### Phase 5: Verification

1.  **Confirm Login:** On Jane's first day, have her attempt to log in with her new credentials.
2.  **Verify Permissions:** Ask her to perform a simple action to confirm her permissions are correct. For example, have her create a test lead. Confirm that she can see what she's supposed to see and *cannot* access administrative sections.
3.  **Troubleshoot:** If there are any issues (e.g., password doesn't work, she can't see leads), use your admin access to diagnose the problem. Check that the user account is "Active," that the permissions are set correctly, and that she is assigned to the correct territory.
