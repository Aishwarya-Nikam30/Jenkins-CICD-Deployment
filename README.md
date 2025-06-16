# 🚀 Node.js CI/CD Pipeline with Jenkins & Docker

A robust and simple Node.js web application demonstrating a complete Continuous Integration/Continuous Delivery (CI/CD) pipeline using **Jenkins** for automation and **Docker** for containerization. This project illustrates how to automate the build, test, and deployment of a Node.js application, promoting efficient and reliable software delivery.

---

## ✨ Features

* **Node.js + Express**: A basic, yet functional web application serving as the project's core.
* **Docker Containerization**: Packages the Node.js application and its dependencies into lightweight, portable containers.
* **Jenkins CI/CD Automation**: Orchestrates the entire development workflow from code commit to deployment.
* **Automated Build & Test**: Ensures code quality and functionality with every change.
* **Automated Deployment**: Streamlines the process of updating the application in a runtime environment.

---

## 🛠 Tech Stack

* **Node.js + Express**: The runtime environment and framework for the web application.
* **Docker**: Used for creating isolated, consistent environments for building and running the application.
* **Jenkins**: The leading open-source automation server, used here to define and execute the CI/CD pipeline.

---

## 📂 Project Structure
/node-js-sample/
├── Dockerfile              # Instructions for building the Docker image
├── Jenkinsfile             # Defines the CI/CD pipeline stages for Jenkins
├── package.json            # Node.js project dependencies and scripts
├── server.js (or index.js) # The main Node.js application file
└── README.md               # Project documentation (this file)

---

## ⚙ Jenkins Pipeline Stages

The `Jenkinsfile` defines a declarative pipeline with the following stages:

1.  ### **Build Stage**
    This stage is responsible for packaging the Node.js application into a Docker image.
    ```bash
    docker build -t node-js-sample .
    ```
    * **Action**: Builds a Docker image from the `Dockerfile` located in the project root.
    * **Output**: A new Docker image tagged `node-js-sample`.

2.  ### **Test Stage**
    This stage runs automated tests within a containerized environment to ensure the application's functionality.
    ```bash
    docker run --rm node-js-sample npm test || true
    ```
    * **Action**: Spins up a temporary container from the `node-js-sample` image and executes the `npm test` script defined in `package.json`.
    * **Note**: The `|| true` ensures the pipeline doesn't stop immediately if tests fail, allowing for potential post-test actions (e.g., publishing test reports). For strict failures, remove `|| true`.
    * **Output**: Test results (logs) from the `npm test` command.

3.  ### **Deploy Stage**
    This stage handles the deployment of the newly built and tested application.
    ```bash
    docker rm -f node-js-sample || true
    docker run -d -p 5000:5000 --name node-js-sample node-js-sample
    ```
    * **Action 1**: Attempts to stop and remove any existing Docker container named `node-js-sample` to ensure a clean deployment of the new version.
    * **Action 2**: Starts a new Docker container in detached mode (`-d`) from the `node-js-sample` image, mapping port `5000` from the container to port `5000` on the host machine.
    * **Output**: A running Docker container serving the Node.js application.

---

## 🚀 Getting Started

### Prerequisites

Make sure you have the following installed on your system where you intend to run or set up this project:

* **Git**: For cloning the repository.
* **Docker**: For building and managing containers.
* **Node.js & npm**: If you plan to run or develop the app locally *without* Docker initially.
* **Jenkins Server**: With Docker installed on the Jenkins agent (or host if running on master) for pipeline execution.

### Run Locally (with Docker)

To run the Dockerized application directly on your local machine:

1.  **Clone the repository:**
    ```bash
    git clone <your-repo-url>
    cd node-js-sample
    ```
2.  **Build the Docker image:**
    ```bash
    docker build -t node-js-sample .
    ```
3.  **Run the Docker container:**
    ```bash
    docker run -d -p 5000:5000 --name node-js-sample node-js-sample
    ```
4.  **Access the application:**
    Open your web browser and visit: `http://localhost:5000`

5.  **Stop the running container (when done):**
    ```bash
    docker stop node-js-sample
    docker rm node-js-sample
    ```

### Set up Jenkins Pipeline

1.  **Ensure Jenkins is running** and Docker is installed on your Jenkins agent.
2.  **Create a New Pipeline Job** in Jenkins.
3.  **Configure the job** to use "Pipeline script from SCM" (Source Code Management).
4.  **Select Git** as your SCM and provide your repository URL.
5.  **Specify `main` (or `master`)** as the branch to build.
6.  **Set the Script Path to `Jenkinsfile`**.
7.  **Save** the job.
8.  **Trigger a build** (e.g., manually or via a webhook from GitHub/GitLab).

---

## 🌐 CI/CD Flow Diagram

```mermaid
graph TD
    A[GitHub Commit / Push] --> B(Jenkins Pipeline Trigger)
    B --> C(Build Docker Image)
    C --> D(Run Tests in Container)
    D --> E(Deploy New Container)
    E --> F[Application Live on Port 5000]

🙏 Acknowledgements
This project was created as part of a DevOps learning journey, demonstrating practical CI/CD implementation. Special thanks to the open-source community for providing the robust tools and examples that made this possible.

💬 Feedback & Contributions
Your suggestions and improvements are always welcome!

Feel free to open an issue if you find bugs or have feature requests.
Submit a pull request if you'd like to contribute directly to the code or documentation.

🚀 Happy CI/CD!
Thank you for checking out this project! I hope it helps you in your DevOps and automation learning journey.

---

🤝 Connect With Me

LinkedIn: (https://www.linkedin.com/in/aishanikam30)
GitHub: (https://github.com/Aishwarya-Nikam30)
Email: (mailto:aishwarya.nikam3009@gmail.com)

---
