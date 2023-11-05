
## 1. Understanding GitOps

GitOps is a paradigm or a set of practices that empowers developers to perform tasks which typically (in traditional IT environments) fall under the purview of IT operations. GitOps involves using Git as a single source of truth for declarative infrastructure and applications. With Git at the center of the delivery pipelines, every change is submitted as a pull request, and no changes are made unless they are committed in Git, ensuring auditability and revertibility.

### Case Study: Weaveworks

Weaveworks, the company that coined the term "GitOps," provides a real-life case study of GitOps in action. By adopting GitOps, Weaveworks reported improvements in productivity and stability. They achieved a deployment frequency that went from weeks to minutes, a drastic reduction in deployment errors due to automated synchronization, and an enhanced developer experience as they could use familiar tools and processes to manage production deployments.

## 2. Building a CI/CD Pipeline

For the purpose of this assignment, I chose to build a CI/CD pipeline using Jenkins, a widely adopted open-source automation server that provides hundreds of plugins to support building, deploying, and automating any project. The pipeline is designed to build and test the backend application, a Spring Boot-based application, upon a Git push event.

### a. Software Tooling

The choice of Jenkins was influenced by its extensive plugin ecosystem, which allows for integrating a wide range of development, testing, and deployment tools. Additionally, Jenkins' robust community support and its ability to work with virtually any type of project make it an ideal choice for CI/CD pipelines.

For source code management, GitHub was used due to its popularity and the ease of integrating with Jenkins through webhooks. Maven was selected as the build tool for its simplicity and effectiveness in managing a project's build lifecycle.

### b. Automated Trigger

The CI/CD pipeline is triggered automatically by a webhook configured in the GitHub repository. When code is pushed to the repository, GitHub sends a POST request to a predefined ngrok URL, which exposes the Jenkins server running on localhost to the internet. This webhook trigger ensures that every Git push initiates a new build and test cycle without manual intervention.

### c. Challenges and Decisions

One of the challenges faced during the setup was exposing the local Jenkins server to GitHub via webhooks, which was resolved using ngrok. Another challenge was ensuring that the Jenkins pipeline script was correctly configured to handle the build and test using the maven-based commands for the project.

The decision to use ngrok was based on its ease of setup and the fact that it provides a secure tunnel to the local Jenkins server.

### d. Pipeline in Action

[Attached video](https://github.com/Faizahamed-S/Enterprise-Programming/raw/main/Assignment5/video1072650939.mp4) shows the pipeline in action. Below is the description of pipeline in action.

1. **Starting the ngrok Server**: Initially, we start the ngrok server on the local machine. This step is crucial as it creates a secure tunnel to the Jenkins server running on localhost, effectively exposing it to the internet while maintaining security. The ngrok server assigns a unique URL that will be used to intercept GitHub webhook requests.

2. **GitHub Push Event**: When a developer commits new code and pushes it to the GitHub repository, it triggers a webhook that has been previously set up.

3. **Webhook Notification**: The push event sends a POST request to the Jenkins server via the unique ngrok URL. This request notifies Jenkins that a change has occurred in the repository, prompting it to start the build process.

4. **Triggering the Jenkins Job**: Upon receiving the webhook notification, Jenkins initiates the pre-configured job. The job begins with checking out the latest code from the GitHub repository to ensure that the build and tests are run against the most recent changes.

5. **Build and Test Execution**: Jenkins then executes the `mvn clean package` command, which compiles the code and packages it into an executable JAR file. Following the build, Jenkins runs the `mvn test` command to carry out the unit tests specified within the project.

6. **Build Success**: If the build and test stages complete without errors, Jenkins reports a SUCCESS status. This indicates that the new changes have been integrated successfully without causing regressions or breaking existing functionality.

Each of these steps is automatically logged by Jenkins, providing a detailed record of the build process. This allows for easy monitoring and troubleshooting, ensuring that any issues can be swiftly addressed and resolved.

