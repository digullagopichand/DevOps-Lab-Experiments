# Week 4 – Install Jenkins on Windows

## Aim
To install and configure Jenkins on Windows OS.

## Description
Jenkins is used to automate software development tasks. This experiment explains how to install Jenkins on Windows and complete its initial configuration.

## Requirements
- Windows operating system
- Jenkins installer (`jenkins.msi`)
- Java installed on the system
- Web browser

## Procedure

### Step 1: Download Jenkins
1. Open the official Jenkins website.
2. Download the Jenkins Windows installer.
3. Save the `jenkins.msi` file.

### Step 2: Run the Installer
1. Run the `jenkins.msi` installation file.
2. Follow the setup wizard.
3. Click **Next** to proceed.
4. Select the installation destination folder.
5. Click **Next**.

### Step 3: Configure the Jenkins Service
1. Select the option to run the service as a local or domain user.
2. Enter the required credentials.
3. Click **Test Credentials**.
4. Click **Next** to continue.

### Step 4: Configure the Port
1. Enter the port number on which Jenkins should run.
2. Click **Test Port** to check availability.
3. Click **Next**.

### Step 5: Select Java and Features
1. Select the directory where Java is installed.
2. Click **Next**.
3. Select the Jenkins features you want to install.
4. Click **Next**.

### Step 6: Install Jenkins
1. Click **Install** to begin installation.
2. Wait until the installation finishes.
3. Click **Finish**.

### Step 7: Unlock Jenkins
1. Open the Jenkins setup page in your browser.
2. Locate the `initialAdminPassword` file in the Jenkins installation data directory shown by the installer.
3. Open the file using Notepad.
4. Copy the password.
5. Paste it into the Administrator password field on the Jenkins unlock page.
6. Click **Continue**.

### Step 8: Customize Jenkins
1. Click **Install suggested plugins**.
2. Wait for the plugins to install.
3. Enter the required information on the Create First Admin User page.
4. Click **Save and Continue**.

### Step 9: Finish Configuration
1. Confirm the Jenkins URL and port on the Instance Configuration page.
2. Click **Save and Finish**.
3. Click **Start using Jenkins** to open the dashboard.

## Files Included
- `experiment-record.pdf` – Lab experiment record
- `README.md` – Experiment documentation
- `images/` – Installation and Jenkins dashboard screenshots

## Expected Output
Jenkins is installed and configured on Windows. The Jenkins dashboard opens successfully in a web browser.

## Result
Jenkins is installed and configured on Windows OS.