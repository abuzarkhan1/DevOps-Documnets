# Automating React CI/CD Pipeline with Jenkins

## Project Setup Using the Following Tools

1. **Node.js**
2. **GitHub**
3. **Jenkins**

---

## Step 1: Jenkins Server Setup on Linux VM

1. **Create Ubuntu VM** using AWS EC2 (t2.medium)
2. **Enable Port 8080** in Security Group Inbound Rules
3. **Connect to the VM** using MobaXterm or SSH
4. **Install Java and Node.js** on the VM:

    ```bash
    sudo apt update
    sudo apt install fontconfig openjdk-17-jre nodejs npm -y
    java -version
    node -v
    npm -v
    ```

5. **Install Jenkins**:

    ```bash
    sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
      https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
    echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
      https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
      /etc/apt/sources.list.d/jenkins.list > /dev/null
    sudo apt-get update
    sudo apt-get install jenkins
    ```

6. **Start Jenkins**:

    ```bash
    sudo systemctl enable jenkins
    sudo systemctl start jenkins
    ```

7. **Verify Jenkins Installation**:

    ```bash
    sudo systemctl status jenkins
    ```

8. **Access Jenkins** in your browser using the VM's public IP:

    ```bash
    http://public-ip:8080/
    ```

9. **Retrieve Jenkins Admin Password**:

    ```bash
    sudo cat /var/lib/jenkins/secrets/initialAdminPassword
    ```

10. **Create Admin Account & Install Required Plugins** in Jenkins

---

## Step 2: Install Node.js Plugin

1. Navigate to **Manage Jenkins** -> **Manage Plugins** -> **Available**.
2. Search for **NodeJS Plugin** and install it.
3. Restart Jenkins if required.

---

## Step 3: Configure Node.js as a Global Tool

1. Navigate to **Manage Jenkins** -> **Global Tool Configuration**.
2. Scroll down to **NodeJS** and click **Add NodeJS**.
3. Provide a name (e.g., `node`) and select the version you want to use.
4. Save the configuration.

---

## Step 4: Create Jenkins Pipeline Job

1. **Create a New Pipeline Job**:
   - Go to the Jenkins dashboard.
   - Click on **New Item**, give it a name, select **Pipeline**, and click **OK**.
   
2. **Scroll Down to the Pipeline Section**:
   - In the Pipeline section, choose **Pipeline script** and paste the following Groovy script:

    ```bash
    pipeline {
        agent any
        tools {
            nodejs 'node'
        }
        stages {
            stage('Checkout') {
                steps {
                    git 'https://github.com/your-repo-name.git'
                }
            }
            stage('Install') {
                steps {
                    sh 'npm install'
                }
            }
            stage('Build') {
                steps {
                    sh 'npm run build'
                }
            }
            stage('Run') {
                steps {
                    sh 'npm start'
                }
            }
        }
    }
    ```

3. **Save the Pipeline Configuration**:
   - Scroll down and click **Save**.

---

## Step 5: Build the Jenkins Job

1. **Trigger the Build**:
   - Go to the Jenkins dashboard.
   - Find your newly created job and click on it.
   - Click **Build Now** on the left-hand side to start the pipeline.

2. **Monitor the Build**:
   - As the pipeline runs, monitor its progress by clicking on the build number in the **Build History** section.
   - View the console output to track each stage's execution.

---

## Step 6: Access the Application in the Browser

1. **Open the Browser**:
   - Once the build is successful, your React application will be running.

2. **Access the Application**:
   - Open your web browser.
   - Enter the URL: `http://public-ip:3000/` (replace `public-ip` with the actual IP of your VM).

3. **Verify the Application**:
   - Ensure that the application is running as expected in the browser.

---

## Congratulations! Your React CI/CD Pipeline is Successfully Set Up and Running 🚀
