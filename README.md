# Toling-website-deployment-automation-with-continuous-integration
Automated deployment of a web tooling solution using Jenkins CI/CD on AWS EC2. Features Java JDK setup, Jenkins installation, security group configuration, and automated build pipelines for seamless web application deployment.

To set up the continuous integration server, an AWS EC2 instance was launched with the following configuration:

1. EC2 Provisioning: Spun up an Ubuntu/Amazon Linux instance dedicated to running Jenkins.
2. Security Group Configuration: Opened port `8080` for Jenkins web UI access alongside SSH (`22`) for administrative access.
3. **Status Verification:** Confirmed that the instance passed health checks and is in a `Running` state.

<img width="554" height="87" alt="image" src="https://github.com/user-attachments/assets/ab298317-4950-4403-bb9d-ed8d887b95ac" />

