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

<img width="554" height="39" alt="image" src="https://github.com/user-attachments/assets/ab631a3d-6ede-474a-a700-319d44a0758a" />


<img width="554" height="401" alt="image" src="https://github.com/user-attachments/assets/2cddf5c2-b674-4aee-a0c5-6593ca717563" />


### Step 2: Accessing the EC2 Instance via SSH

Connected to the running Jenkins EC2 server via SSH using PowerShell:
ssh -i "C:\Users\lenovo\Downloads\jenkins.pem" ubuntu@13.63.175.50

<img width="554" height="401" alt="image" src="https://github.com/user-attachments/assets/97112128-7a31-49a9-a44d-ee4441abe576" />

### Step 3: Updating Package Index

Updated the local package repository index to ensure the latest package lists and dependencies are retrieved:
sudo apt update

<img width="553" height="284" alt="image" src="https://github.com/user-attachments/assets/17d88be0-fabc-499d-8bd2-17f5a719b760" />

### Step 4: Installing OpenJDK

Jenkins requires Java to run. Installed the headless Java Development Kit (JDK) package:
sudo apt install -y default-jdk-headless 

<img width="554" height="39" alt="image" src="https://github.com/user-attachments/assets/2c529a2e-37ab-4437-a959-7c94299b5d7f" />

I tried using this command  wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -  but it returned command not found. 

<img width="553" height="112" alt="image" src="https://github.com/user-attachments/assets/d65dddb6-4255-4053-868f-bf3096e5a73c" />

<img width="553" height="240" alt="image" src="https://github.com/user-attachments/assets/ba6120ee-feef-476c-aa2a-a95191e0a6ec" />

<img width="533" height="193" alt="image" src="https://github.com/user-attachments/assets/9881efdd-63dc-48eb-84ea-eba3931f6569" />

When wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add - command returned command not found I used the command  sudo apt update it did not work as a result I removed the old Jenkins repository and used the following commands 
 sudo rm -f /etc/apt/sources.list.d/jenkins.list

sudo rm -f /etc/apt/keyrings/jenkins-keyring.asc

sudo mkdir -p /etc/apt/keyrings
C
url -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo gpg --dearmor -o /etc/apt/keyrings/jenkins.gpg

echo "deb [signed-by=/etc/apt/keyrings/jenkins.gpg] https://pkg.jenkins.io/debian-stable binary/" | sudo tee /etc/apt/sources.list.d/jenkins.list

deb [signed-by=/etc/apt/keyrings/jenkins.gpg] https://pkg.jenkins.io/debian-stable binary/

<img width="554" height="238" alt="image" src="https://github.com/user-attachments/assets/bc7fd1d2-15f6-432f-ab96-2dfe7aa5aa79" />

sudo apt update(gave me an error because my system still has the old key)

As a result I used 

sudo rm -f /etc/apt/keyrings/jenkins.gpg

sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \https://pkg.jenkins.io/debian-stable/jenkins.io-2026.key
 
echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/" | sudo tee /etc/apt/sources.list.d/jenkins.list

deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ to replace old key with the new key. 

<img width="554" height="166" alt="image" src="https://github.com/user-attachments/assets/1bbd28bd-6aaa-413d-9f80-931d0bb3fc61" />

I used sudo sysyemctl status jenkins to check if Jenkins is active 

<img width="553" height="336" alt="image" src="https://github.com/user-attachments/assets/ab28844b-724d-4495-9f52-51aafa27c51a" />

Unlocking Jenkins required me to access password so I used the command: sudo cat /var/lib/jenkins/secrets/initialAdminPassword and it returned 

369bc179662249d7ac07428c2a843cd2 

<img width="554" height="333" alt="image" src="https://github.com/user-attachments/assets/7e147f0c-b71c-49a2-981e-c999f852d701" />

Finally logged into Jenkins 

<img width="554" height="298" alt="image" src="https://github.com/user-attachments/assets/210c1605-f53c-488d-b248-2e167d3c85ae" />

<img width="554" height="339" alt="image" src="https://github.com/user-attachments/assets/2ccbf411-5a92-4573-9e20-812637e8c7d2" />

I created first user admin 

<img width="554" height="335" alt="image" src="https://github.com/user-attachments/assets/9566ec6a-2d4c-4d07-bd93-36139b742eb0" />


<img width="554" height="334" alt="image" src="https://github.com/user-attachments/assets/3e2869fc-9c69-494d-b61a-f48924cfe35a" />

Finally Jenkins was ready



Testing Jenkins webhook - August 10
