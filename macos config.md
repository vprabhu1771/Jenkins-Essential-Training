echo $PATH

To use `/opt/homebrew/bin/php` in Jenkins, you need to ensure Jenkins has this path included in its environment variables. Here’s how you can configure Jenkins to recognize PHP at `/opt/homebrew/bin/php`:

### 1. Add PHP Path to Jenkins Environment

#### Option A: Configure Jenkins Global Environment Variables

1. **Open Jenkins Dashboard**:
   - Go to your Jenkins URL in a web browser.

2. **Navigate to Manage Jenkins**:
   - Click on "Manage Jenkins" from the left sidebar.

3. **Configure System**:
   - Click on "Configure System".

4. **Global Properties**:
   - Scroll down to the "Global properties" section.
   - Check the "Environment variables" option if it isn’t already checked.

5. **Add New Environment Variable**:
   - Click "Add" under Environment variables.
   - Set `Name` to `PATH`.
   - Set `Value` to include `/opt/homebrew/bin`, along with the existing PATH. For example:
     ```
     /opt/homebrew/bin:/usr/local/bin:/usr/bin:/bin
     ```

6. **Save Changes**:
   - Click "Save" to apply these settings.

7. **Restart Jenkins** (if necessary):
   - Some systems might require a restart of Jenkins to apply the new environment settings. 

#### Option B: Configure PATH in Jenkins Job

1. **Edit Jenkins Job**:
   - Go to the job configuration page for your specific build job.

2. **Build Environment**:
   - Under the "Build Environment" section, check "Inject environment variables to the build process".

3. **Properties Content**:
   - Add a custom environment variable for PATH:
     ```
     PATH=/opt/homebrew/bin:/usr/local/bin:/usr/bin:/bin
     ```

4. **Save Changes**:
   - Click "Save" to update the job configuration.

### 2. Use the Full Path in Shell Command

If you prefer not to modify the global PATH, you can directly specify the full path to PHP in your Jenkins build script:

1. **Edit the Build Step**:
   - In the Jenkins job configuration, locate the "Build" step where you have your shell script.

2. **Update Command**:
   - Replace `php artisan migrate` with the full path `/opt/homebrew/bin/php artisan migrate`.

   ```bash
   /opt/homebrew/bin/php artisan migrate
   ```

3. **Save the Job**:
   - Save the configuration changes.

### 3. Test the Configuration

After making these changes:

1. **Run the Job**:
   - Trigger a build for your job in Jenkins.

2. **Check the Console Output**:
   - View the console output to verify that the build is using `/opt/homebrew/bin/php` and running `php artisan migrate` successfully.

By following these steps, Jenkins should correctly use PHP from `/opt/homebrew/bin/php`.
