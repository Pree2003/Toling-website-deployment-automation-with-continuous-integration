# Toling-website-deployment-automation-with-continuous-integration
Automated deployment of a web tooling solution using Jenkins CI/CD on AWS EC2. Features Java JDK setup, Jenkins installation, security group configuration, and automated build pipelines for seamless web application deployment.

To set up the continuous integration server, an AWS EC2 instance was launched with the following configuration:

1. EC2 Provisioning: Spun up an Ubuntu/Amazon Linux instance dedicated to running Jenkins.
2. Security Group Configuration: Opened port `8080` for Jenkins web UI access alongside SSH (`22`) for administrative access.
3. Status Verification: Confirmed that the instance passed health checks and is in a `Running` state.

<img width="554" height="87" alt="image" src="https://github.com/user-attachments/assets/ab298317-4950-4403-bb9d-ed8d887b95ac" />

<img width="554" height="66" alt="image" src="https://github.com/user-attachments/assets/141754ec-a5ba-4d50-a210-75af6fdf4a6e" />

<img width="554" height="249" alt="image" src="https://github.com/user-attachments/assets/02a411d0-6be0-4b09-9aef-d13bcafd561f" />

Next step I installed JDK 


<img width="554" height="522" alt="image" src="https://github.com/user-attachments/assets/868ec55c-d80d-4f9e-8797-fbfdd05ae392" />

<img width="554" height="401" alt="image" src="https://github.com/user-attachments/assets/2cddf5c2-b674-4aee-a0c5-6593ca717563" />


### Step 2: Accessing the EC2 Instance via SSH

Connected to the running Jenkins EC2 server via SSH using PowerShell:
ssh -i "C:\Users\lenovo\Downloads\jenkins.pem" ubuntu@13.63.175.50

<img width="554" height="401" alt="image" src="https://github.com/user-attachments/assets/97112128-7a31-49a9-a44d-ee4441abe576" />

### Step 3: Updating Package Index

Updated the local package repository index to ensure the latest package lists and dependencies are retrieved:
sudo apt update
