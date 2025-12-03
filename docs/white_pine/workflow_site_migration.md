# Workflow: Creating a Local Backup & Git Repository for mnaatjes.com

This document outlines the step-by-step process for securely backing up your live WordPress site from Bluehost and storing the codebase in a new Git repository for local development and version control.

---

### **Phase 1: Backing Up the Live Website Files**

In this phase, we will connect to your server via SSH to compress your website files into a single archive and then download it.

1.  **Connect to Your Server via SSH:**
    *   Open your local terminal (Windows Terminal, etc.).
    *   Use the SSH command from your documentation to connect. This command specifies your private key for authentication.
        ```bash
        ssh -i C:\Users\micha\.ssh\win_11_home_rsa pwmpmemy@50.6.19.171
        ```

2.  **Create a Compressed Archive of Your Site:**
    *   Once logged in, you will be in your home directory (`/home2/pwmpmemy/`).
    *   Your website files are in the `public_html` directory. Use the `tar` command to create a single compressed `.tar.gz` file. This is much faster than downloading thousands of individual files.
        ```bash
        tar -czvf mnaatjes_files_backup.tar.gz public_html/
        ```
    *   This command will create a file named `mnaatjes_files_backup.tar.gz` in your home directory.

3.  **Download the Archive to Your Local Machine:**
    *   Disconnect from the SSH session by typing `exit`.
    *   Now, from your local terminal, use the `scp` (Secure Copy) command to download the archive you just created. The `.` at the end of the command tells it to download the file to your current local directory.
        ```bash
        scp -i C:\Users\micha\.ssh\win_11_home_rsa pwmpmemy@50.6.19.171:~/mnaatjes_files_backup.tar.gz .
        ```

4.  **Clean Up the Remote Server:**
    *   Log back into your server via SSH one more time.
    *   Remove the temporary archive file to save space.
        ```bash
        rm mnaatjes_files_backup.tar.gz
        ```
    *   Type `exit` to disconnect.

---

### **Phase 2: Backing Up the WordPress Database**

This phase uses the cPanel tools described in your documentation to export the site's database.

1.  **Log in to Bluehost** and navigate to **cPanel**.
2.  Find and click the **"phpMyAdmin"** icon.
3.  **Identify Your Database:** In the left-hand sidebar of phpMyAdmin, you will see one or more database names. Your WordPress site's database name is defined in the `wp-config.php` file. You can now look at this file locally inside the `public_html` folder you backed up. Find the line that looks like this:
    ```php
    define( 'DB_NAME', 'databasename_goes_here' );
    ```
4.  **Export the Database:**
    *   In phpMyAdmin, click on the name of your WordPress database from the list on the left.
    *   Click the **"Export"** tab at the top of the main panel.
    *   For **Export Method**, choose **"Quick"**.
    *   For **Format**, ensure **"SQL"** is selected.
    *   Click **"Go"**. Your browser will download a `.sql` file containing your entire database. Save this file in a memorable location.

---

### **Phase 3: Setting Up the Local Git Repository**

Now we will organize the files and create a version-controlled project.

1.  **Create a Project Folder:** On your local machine, create a new folder for your project (e.g., `mnaatjes-com-site`).
2.  **Extract Files:** Unzip the `mnaatjes_files_backup.tar.gz` archive. This will create a `public_html` folder. Move all the contents *from inside* `public_html` into your new `mnaatjes-com-site` project folder.
3.  **Initialize Git:** Open your terminal, navigate *inside* the `mnaatjes-com-site` folder, and run:
    ```bash
    git init
    ```
4.  **Create a `.gitignore` File:** This is a critical step for any WordPress project to avoid committing unnecessary or sensitive files. Create a file named `.gitignore` in the root of your project folder and paste the following content into it:
    ```
    # WordPress
    wp-config.php
    wp-content/uploads/
    wp-content/blogs.dir/
    wp-content/upgrade/
    wp-content/backup-db/
    sitemap.xml
    sitemap.xml.gz

    # Thumbs, IDE/OS files
    *.log
    .DS_Store
    Thumbs.db
    .idea/
    .vscode/
    ```
5.  **Create a Database Backup Folder:** Inside your project, create a new folder named `database_backups`. Move the `.sql` file you downloaded in Phase 2 into this folder. (Note: The `.gitignore` file should be updated to include `database_backups/` if you don't want to commit the SQL file).
6.  **Commit Your Code:** Now, stage and commit your files.
    ```bash
    git add .
    git commit -m "Initial commit of mnaatjes.com source"
    ```
7.  **Push to GitHub:**
    *   Go to GitHub and create a new, empty repository (e.g., `mnaatjes-com`).
    *   Follow the instructions on GitHub to add the remote URL to your local repository and push your commit. The commands will look something like this:
        ```bash
        git remote add origin https://github.com/mnaatjes/mnaatjes-com.git
        git branch -M main
        git push -u origin main
        ```

### **Conclusion**

At the end of this process, you will have a complete backup of your site's files and database stored safely on your local machine, and your entire codebase will be version-controlled in a clean Git repository, ready for local development.
