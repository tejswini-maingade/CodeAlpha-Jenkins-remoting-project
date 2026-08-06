# 🚀 Jenkins Remoting with SSH-Based Remote Agent

> A hands-on DevOps project demonstrating how Jenkins distributes build workloads from a Controller to a remote Ubuntu Agent using Jenkins Remoting over SSH.

![Jenkins](https://img.shields.io/badge/Jenkins-CI%2FCD-red?logo=jenkins)
![Ubuntu](https://img.shields.io/badge/Ubuntu-26.04-orange?logo=ubuntu)
![Java](https://img.shields.io/badge/Java-21-blue?logo=openjdk)
![License](https://img.shields.io/badge/License-MIT-green)

---

# 📖 Project Overview

Modern CI/CD environments rarely execute all builds on a single machine. Jenkins solves this challenge using a **Controller-Agent architecture**, where the controller manages jobs while remote agents perform the actual build execution.

In this project, a remote Ubuntu EC2 instance is connected to the Jenkins Controller using **SSH-based Jenkins Remoting**, enabling secure, distributed, and scalable build execution.

---

# 🎯 Objectives

- Configure a Jenkins Controller and remote Agent
- Connect the agent using SSH key authentication
- Execute Jenkins pipelines on a remote machine
- Understand Jenkins Remoting architecture
- Learn distributed build execution
- Improve security using node isolation
- Gain practical CI/CD experience

---

# 🛠️ Technologies Used

| Technology | Purpose |
|------------|---------|
| Jenkins | CI/CD Automation |
| Jenkins Remoting | Controller-Agent Communication |
| Ubuntu 26.04 LTS | Controller & Agent OS |
| OpenJDK 21 | Java Runtime |
| SSH | Secure Agent Communication |
| Git | Version Control |
| GitHub | Project Hosting |
| AWS EC2 | Cloud Infrastructure |

---

# 🏗️ Architecture

```text
                    +---------------------------+
                    |        Developer          |
                    +-------------+-------------+
                                  |
                                  |
                           Trigger Build
                                  |
                                  ▼
                  +-------------------------------+
                  |      Jenkins Controller       |
                  |  Job Scheduling & Management  |
                  +---------------+---------------+
                                  |
                   SSH + Jenkins Remoting
                                  |
                                  ▼
                  +-------------------------------+
                  |      Ubuntu Jenkins Agent     |
                  |     Build Execution Node      |
                  +---------------+---------------+
                                  |
                                  ▼
                    Execute Pipeline Commands
                     • hostname
                     • whoami
                     • uname -a
                     • Build Steps
                                  |
                                  ▼
                  +-------------------------------+
                  | Build Logs & Status Returned  |
                  +---------------+---------------+
                                  |
                                  ▼
                           ✅ BUILD SUCCESS
```

---

# 🔄 Workflow

```text
Developer
    │
    ▼
Push Code / Build Now
    │
    ▼
Jenkins Controller
    │
    ▼
Find Agent (Label: linux)
    │
    ▼
SSH Authentication
    │
    ▼
Launch Jenkins Remoting
    │
    ▼
Create Workspace
    │
    ▼
Execute Pipeline
    │
    ▼
Collect Logs
    │
    ▼
Display Console Output
    │
    ▼
SUCCESS
```

---

# ⚙️ Jenkins Pipeline

```groovy
pipeline {
    agent {
        label 'linux'
    }

    stages {

        stage('System Information') {
            steps {
                sh 'echo "Hostname:"'
                sh 'hostname'

                sh 'echo "Current User:"'
                sh 'whoami'

                sh 'echo "Operating System:"'
                sh 'uname -a'
            }
        }

        stage('Workspace Details') {
            steps {
                sh 'pwd'
                sh 'ls -la'
            }
        }

        stage('Verification') {
            steps {
                sh 'echo "🚀 Remote build executed successfully!"'
            }
        }
    }
}
```

---

# 📋 Project Workflow Explained

### Step 1

Jenkins Controller receives a build request.

⬇️

### Step 2

Controller searches for an available agent using the label:

```text
linux
```

⬇️

### Step 3

The Controller authenticates to the remote Ubuntu Agent using **SSH Key Authentication**.

⬇️

### Step 4

Jenkins automatically copies the **Remoting Agent (agent.jar)** and establishes communication.

⬇️

### Step 5

A workspace is created on the remote machine.

⬇️

### Step 6

Pipeline commands execute remotely.

⬇️

### Step 7

Logs and build status are streamed back to the Controller.

⬇️

### Step 8

Build completes successfully.

---

# 📂 Repository Structure

```text
Jenkins-Remoting-Project/
│
├── README.md
│
├── Jenkinsfile
│
├── architecture/
│   └── architecture-diagram.png
│
│
└── report/
    └── Jenkins_Remoting_Project_Report.pdf
```

---

# 📸 Project Screenshots

| Screenshot | Description |
|------------|-------------|
| EC2 Instances | Controller & Agent running |
| Jenkins Dashboard | Jenkins Home |
| Node Configuration | Agent Settings |
| Agent Online | Connected Agent |
| Agent Logs | SSH & Remoting Connection |
| Pipeline | Jenkinsfile |
| Build History | Successful Builds |
| Console Output | Remote Execution |
| Agent Workspace | Workspace created remotely |

---

# 🔐 Security Features

## SSH Key Authentication

Instead of passwords, Jenkins authenticates using SSH key pairs.

Advantages:

- Secure
- Password-less authentication
- Industry best practice
- Easier automation

---

## Dedicated Agent User

```text
jenkins-agent
```

Builds execute using a dedicated non-root user.

---

## Node Isolation

```
Controller
    ↓
Schedules Jobs

Agent
    ↓
Executes Jobs
```

This minimizes risk to the Jenkins Controller.

---

# ✅ Build Verification

Successful build execution confirms:

- Jenkins Controller connected successfully
- SSH authentication succeeded
- Jenkins Remoting launched
- Workspace created on Agent
- Commands executed remotely
- Console logs returned
- Build completed successfully

Sample console output:

```text
Running on agent-linux

Hostname:
ip-172-31-0-43

Current User:
jenkins-agent

Operating System:
Linux 7.x x86_64 GNU/Linux

Workspace:
/home/jenkins-agent/workspace/remote-build

🚀 Remote build executed successfully!

Finished: SUCCESS
```

---

# 📚 Key Learnings

- Jenkins Controller-Agent Architecture
- Jenkins Remoting
- Distributed Builds
- SSH Key Authentication
- Jenkins Nodes
- Pipeline as Code
- Remote Build Execution
- CI/CD Fundamentals
- Build Isolation
- Secure Automation

---

# 🚀 Future Enhancements

- Docker-based builds
- Kubernetes Agents
- Dynamic Cloud Agents
- Multi-Agent Pipelines
- Parallel Builds
- Artifact Archiving
- Slack Notifications
- Email Notifications
- SonarQube Integration
- Docker Image Build & Push

---

# 🎉 Conclusion

This project successfully demonstrates how **Jenkins Remoting** enables distributed CI/CD by connecting a remote Ubuntu agent to a Jenkins Controller using **SSH-based authentication**.

The Controller schedules and manages jobs, while the remote Agent executes pipeline tasks and streams logs back to Jenkins. This architecture improves scalability, enhances security through node isolation, and reflects real-world DevOps practices used in production environments.

This hands-on implementation strengthened my understanding of Jenkins Controller-Agent architecture, SSH-based authentication, distributed builds, and practical CI/CD automation.

---

## ⭐ If you found this project helpful, consider giving it a Star!
