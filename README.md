# Python App CI/CD with Jenkins and AWS EC2

This project demonstrates how to deploy a Python application on **AWS EC2** using **Jenkins Pipeline** and **GitHub**.

---

## 🚀 Architecture
- **Server 1 (Jenkins Server)**  
  - Runs Jenkins.  
  - Pulls source code from GitHub.  
  - Deploys application to remote EC2 server via SSH.  

- **Server 2 (App Server)**  
  - Runs the Python application.  
  - Receives code and dependencies from Jenkins.  

- **GitHub**  
  - Stores the application code and Jenkins pipeline (`Jenkinsfile`).  

---

## 🛠️ Prerequisites
1. Two AWS EC2 instances:
   - **Jenkins Server** (Ubuntu 22.04 recommended).
   - **Python App Server** (Ubuntu 22.04 with Python 3.12+).  

2. Installed on Jenkins Server:
   - Jenkins  
   - Git  
   - SSH keys (added to Jenkins credentials)  

3. Installed on App Server:
   - Python 3.12+  
   - `python3-pip`, `python3-venv`  
   - OpenSSH (`openssh-server`, `openssh-client`)  
   - Security group opened for app port (e.g., 5000)  

---

## ⚙️ Jenkins Pipeline
The CI/CD pipeline is defined in the `Jenkinsfile`:

1. **Clone Repo**  
   - Pulls the latest code from GitHub.  

2. **Deploy to Server**  
   - Connects to the App Server via SSH.  
   - Creates the app directory and copies code/files.  

3. **Install & Run App**  
   - Installs dependencies in a Python virtual environment.  
   - Starts the application using `nohup`.  

---

## ▶️ How to Run

1. Push your code and `Jenkinsfile` to GitHub.  
2. Configure a Jenkins Pipeline job linked to this repository.  
3. Add EC2 server credentials in Jenkins:  
   - **Kind**: SSH Username with private key  
   - **ID**: `SERVER1`  
   - **Username**: `ubuntu`  
   - **Private Key**: contents of your `.pem` file  

4. Run the pipeline in Jenkins.  
5. Access the app in your browser at:  

http://<APP_SERVER_PUBLIC_IP>:5000


---

## 📂 Project Structure


.
├── app.py # Main Python app
├── requirements.txt # Python dependencies
├── Dockerfile # (Optional) Docker setup
├── Jenkinsfile # CI/CD pipeline
├── README.md # Documentation
└── test/ # Tests

---

## 📝 Notes
- Each deployment uses `nohup` to run the app in the background.  
- You may want to use `systemd` or `Docker` for production deployments.  
- Ensure old processes are cleaned up if re-running multiple times.  

---