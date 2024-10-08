# Jenkins-Essential-Training

[Jenkins](https://www.jenkins.io/) is an open-source automation server that enables developers to build, test, and deploy their software reliably. This document provides an overview of how to set up and use Jenkins for continuous integration and continuous deployment (CI/CD) pipelines.
 
## Table of Contents
1. [Download and Install cygwin](https://github.com/vprabhu1771/Jenkins-Essential-Training/tree/main/1%20-%20Download%20and%20Install%20cygwin)

2. [Download and Install Python](https://github.com/vprabhu1771/Jenkins-Essential-Training/tree/main/2%20-%20Download%20and%20Install%20Python)

3. [Download and Install Java JDK](https://github.com/vprabhu1771/Jenkins-Essential-Training/tree/main/3%20-%20Download%20and%20Install%20Java%20JDK)

4. [Download and Install Jenkins](https://github.com/vprabhu1771/Jenkins-Essential-Training/tree/main/1%20-%20Download%20and%20Install%20Jenkins)

5. [Create your first Jenkins Pipeline Hello World](https://github.com/vprabhu1771/Jenkins-Essential-Training/tree/main/2%20-%20Create%20your%20first%20Jenkins%20Pipeline%20Hello%20World)

6. [First Java Program in Jenkins](https://github.com/vprabhu1771/Jenkins-Essential-Training/tree/main/3%20-%20First%20Java%20Program%20in%20Jenkins)


## Prerequisites

Before setting up Jenkins, ensure you have the following:

- A server or a machine with sufficient resources (recommended at least 1GB RAM, 1 CPU)
- Java Development Kit (JDK) installed (Jenkins requires Java 11 or newer)
- Administrative privileges to install software

## Installation

### Installing Jenkins on macOS

1. Download and Install: [HomeBrew](https://formulae.brew.sh/formula/jenkins#default)

```
brew install jenkins
```

Note: When using launchctl the port will be 8080.

To start jenkins now and restart at login:

```
brew services start jenkins
```

Or, if you don't want/need a background service you can just run:

```
/opt/homebrew/opt/jenkins/bin/jenkins --httpListenAddress\=127.0.0.1 --httpPort\=8080
```

```
/Users/mac_rig2/.jenkins/secrets/initialAdminPassword
```

### Installing Jenkins on Ubuntu/Debian

1. Update your system:
    ```bash
    sudo apt update
    sudo apt install openjdk-11-jdk -y
    ```
2. Add Jenkins repository and import the GPG key:
    ```bash
    wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
    sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
    ```
3. Install Jenkins:
    ```bash
    sudo apt update
    sudo apt install jenkins -y
    ```

4. Start Jenkins and enable it to start at boot:
    ```bash
    sudo systemctl start jenkins
    sudo systemctl enable jenkins
    ```

### Installing Jenkins on Windows

1. Download the [Jenkins Windows installer](https://www.jenkins.io/download/) from the official Jenkins website.
2. Run the installer and follow the on-screen instructions.
3. Ensure the installer installs Jenkins as a Windows service.

## Basic Configuration

1. **Access Jenkins**: Open a web browser and go to `http://<your-server-ip>:8080`.

2. **Unlock Jenkins**: Enter the initial admin password found in:
   - **Ubuntu/Debian**: `/var/lib/jenkins/secrets/initialAdminPassword`
   - **Windows**: `C:\Program Files (x86)\Jenkins\secrets\initialAdminPassword`

3. **Customize Jenkins**: Install the recommended plugins or select the plugins you need.

4. **Create an Admin User**: Follow the setup wizard to create your first admin user.

## Setting Up a Jenkins Pipeline

### Using Declarative Pipeline Syntax

Jenkins supports two types of syntax for defining pipelines: Declarative and Scripted. The declarative pipeline is recommended for simpler, structured pipelines.

### Example Jenkinsfile

Create a file named `Jenkinsfile` in the root of your repository:

```groovy
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                // Add your build commands here
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                // Add your test commands here
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
                // Add your deploy commands here
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            // Add any cleanup tasks here
        }
    }
}
```
