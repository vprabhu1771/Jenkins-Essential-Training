```
https://plugins.jenkins.io/publish-over-ftp/
```

The "Send build artifacts over FTP" option is missing because the **Publish Over FTP plugin is not installed**, or it's not enabled for your project type.

Here's how to fix it and understand the options:

---

## 🔧 1. Install the Plugin

First, verify the plugin is installed:

1. Go to **Manage Jenkins** → **Manage Plugins**.
2. Click the **Installed** tab and search for **Publish Over FTP**.
3. If not found, go to the **Available** tab, search for it, select it, and install it .

After installation, you'll need to restart Jenkins for the plugin to take effect.

---

## ⚙️ 2. Global Configuration

Before the option appears in jobs, you must configure at least one FTP server globally:

1. Go to **Manage Jenkins** → **Configure System**.
2. Find the **Publish over FTP** section.
3. Click **Add** and fill in:
   - **FTP Server Name**: A name for this server (used later in jobs).
   - **Hostname**: IP or domain.
   - **Username / Password**: FTP credentials.
   - **Remote Directory**: Set this to `/` to keep it flexible, then define subdirectories per job .
4. Click **Test Configuration** to verify the connection, then **Save**.

---

## 📂 3. Where to Find It in a Freestyle Job

Once the plugin is installed and configured, the option appears in your job configuration:

1. Open your job and click **Configure**.
2. Scroll down to the **Post-build Actions** section.
3. Click **Add post-build action** and select **Send build artifacts over FTP** from the dropdown .

> **Note**: This plugin was originally designed as a **post-build action** only. If you need it as a build step during the build process, there is an open feature request for this . As a workaround, you can use the **Flexible Publish** plugin to make it conditional, or switch to a Pipeline where the `ftpPublisher` step works as a build step.

---

## 🧪 4. If You're Using a Pipeline Project

In Pipeline jobs, the "Post-build Actions" section doesn't exist at all — you use the `ftpPublisher` step in your Jenkinsfile instead.

You can generate the correct Pipeline syntax:

1. Open your Pipeline job and click **Pipeline Syntax** from the left menu.
2. Select **ftpPublisher: send build artifacts over FTP** from the dropdown.
3. Configure the transfer settings.
4. Click **Generate Pipeline Script** to get the code .

Example Pipeline snippet:

```groovy
stage('Upload via FTP') {
    steps {
        ftpPublisher(
            publishers: [[
                configName: 'your-ftp-config-name',
                transfers: [[
                    sourceFiles: 'dist/**',
                    removePrefix: 'dist',
                    remoteDirectory: 'public_html'
                ]]
            ]]
        )
    }
}
```

---

## 🚨 Common Issues

| Issue | Solution |
|-------|----------|
| Plugin installed but option not showing | Restart Jenkins after installation |
| Option appears but transfers 0 files | Check your **Source files** pattern (use Ant-style patterns like `**/*.jar`)  |
| "FTP Server Name" dropdown empty | You haven't configured a server in **Configure System** yet |
| Using a Pipeline project | Use `ftpPublisher` step in Jenkinsfile — post-build actions aren't available |

Let me know if you're still having trouble after installing the plugin — I can help with the specific error or job type you're using.


-----
```
Jenkins -> Manage Jenkins -> System -> Publish over FTP
```
FTP Servers

Name: `Bughunt FTP`

Hostname: `bughunt.in`

Username: `cpanel_username`

Password: `cpanel_password`

Remote Directory: `/`

Click `Test Configuration`


# Build Config

```
Jenkins -> bughunt.in -> Configure -> Build Steps
```

# Execute Windows batch command 

```
npm run build
```

# Send files over FTP


FTP Publishers -> FTP Server

Name -> `Bughunt FTP`


Transfers -> Transfer Set

Source files -> `dist/**`

Remove prefix -> `dist`

Remote directory -> `public_html`


