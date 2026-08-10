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

<img width="337" height="362" alt="image" src="https://github.com/user-attachments/assets/4c423009-cbb5-4e3d-820b-ec0ecdcf95ad" />

<img width="554" height="114" alt="image" src="https://github.com/user-attachments/assets/0fcd57e9-d10b-472a-bd67-1c79e15b92fa" />

I added webhook to my repository 


<img width="554" height="398" alt="image" src="https://github.com/user-attachments/assets/6af3c48a-2c77-4520-ad48-df0dabde5b7b" />

I created freestyle project 

<img width="554" height="331" alt="image" src="https://github.com/user-attachments/assets/6025f856-1739-4cf3-97ad-ab80a2302972" />

<img width="183" height="102" alt="image" src="https://github.com/user-attachments/assets/b4c4b326-fc0b-4c18-aba0-0a60641be9b0" />

<img width="553" height="223" alt="image" src="https://github.com/user-attachments/assets/d4dea78c-37a9-402a-859d-8f9ddab9dfb1" />

<img width="554" height="219" alt="image" src="https://github.com/user-attachments/assets/3da37897-2ef1-44c3-9161-5ed0c35c14b0" />

Web console of #2 & #3

<img width="554" height="212" alt="image" src="https://github.com/user-attachments/assets/b9b95756-3397-4fb6-8c21-838042f454c9" />

I created personal token (classic) so that I can add it to my credentials in Jenkins


<img width="554" height="200" alt="image" src="https://github.com/user-attachments/assets/2f5e4f6f-1b1c-4c26-8e59-7da68dc41431" />

Github hook trigger

The GitHub hook trigger for GITScm polling is used to automatically notify Jenkins when something changes in a GitHub repository.

<img width="543" height="606" alt="image" src="https://github.com/user-attachments/assets/1fe572a1-1c0b-4185-8f52-d03e4c7d4912" />

<img width="554" height="216" alt="image" src="https://github.com/user-attachments/assets/31fa2c59-fe55-4c82-bdef-bc48c1c154c8" />


I tried to test configuration but it failed because a problem occurred while processing the request. This happened because Jenkins is failing before it even gets to the SSH connection.

<img width="554" height="43" alt="image" src="https://github.com/user-attachments/assets/2755d98d-e915-4e57-a484-dcda17f856b7" />

My next step was to run  sudo journalctl -u jenkins --since "5 minutes ago" --no-pager so it can show me what happened when I clicked Test configuration. java.lang.NoSuchMethodError:
jenkins.plugins.publish_over_ssh.BapSshHostConfiguration.setCommonConfig(java.lang.Object) This message indicates that a version mismatch between the Publish Over SSH plugin and its required Publish Over X infrastructure plugin.

<img width="554" height="239" alt="image" src="https://github.com/user-attachments/assets/0a4bf5f6-b146-4119-a056-1ed81baffade" />

Next step is to fix the plugin by going to the manage Jenkins settings to search for the versions of  Publish Over SSH & Publish Over X and I found that they are the current working versions. 

<img width="554" height="351" alt="image" src="https://github.com/user-attachments/assets/f9523730-da6b-44c2-855b-e8ad998450dd" />

<img width="554" height="217" alt="image" src="https://github.com/user-attachments/assets/b0c89355-a939-4ddb-8de4-1eda4c7dd359" />

<img width="554" height="262" alt="image" src="https://github.com/user-attachments/assets/ee34e188-3407-4155-b864-e7d95cf95171" />

Finally testing configuration became a success


<img width="554" height="205" alt="image" src="https://github.com/user-attachments/assets/9c06ed3a-d50f-4a56-a1c2-a11ebe185e65" />

<img width="158" height="62" alt="image" src="https://github.com/user-attachments/assets/d05228bf-8fac-4853-a044-63331289f771" />


<img width="553" height="304" alt="image" src="https://github.com/user-attachments/assets/3f1aace2-d0ea-4140-af3c-04c375d7d3bc" />


<img width="187" height="103" alt="image" src="https://github.com/user-attachments/assets/b3af1993-c9e6-48cd-9ad3-4a1fa7ce4dae" />

<img width="552" height="453" alt="image" src="https://github.com/user-attachments/assets/598bf81f-09cc-4b56-932b-b974cb994f40" />


Jenkins Artifact Deployment to NFS Server
The objective of this stage was to configure Jenkins to automatically transfer the README.md artifact from the Jenkins server to the NFS server using Publish Over SSH.
1.Verify the NFS Directory

<img width="388" height="38" alt="image" src="https://github.com/user-attachments/assets/6429262a-e9b7-4201-ac0e-a8e0a99bab7e" />

After connecting to the NFS server using SSH, I first checked whether the /mnt/apps directory existed:
ls -ld /mnt/apps
Initially, the directory was owned by root:
drwxr-xr-x. 4 root root 49 Jun 23 00:00 /mnt/apps
I also checked its contents:
ls -l /mnt/apps
The directory contained:cgi-bin ,html and test.txt .However, README.md was not present.

2.Test Directory Permissions

<img width="504" height="54" alt="image" src="https://github.com/user-attachments/assets/b17815c3-2d31-4fe3-891a-28164eb9011d" />


Because Jenkins was unable to publish the artifact, I investigated the permissions on /mnt/apps.
I changed the ownership of the directory to ec2-user:
sudo chown ec2-user:ec2-user /mnt/apps
I then verified the change:
ls -ld /mnt/apps
The result showed:
drwxr-xr-x. 4 ec2-user ec2-user 49 Jun 23 00:00 /mnt/apps

3. Test Write Access

<img width="513" height="238" alt="image" src="https://github.com/user-attachments/assets/3eff8280-4659-4923-bc5d-43d7156004af" />

Before testing Jenkins again, I confirmed that the ec2-user could write to /mnt/apps.
I created a temporary test file:
touch /mnt/apps/test-jenkins.txt
Then I verified that it existed:
ls -l /mnt/apps/test-jenkins.txt
The output confirmed that the file was successfully created:
-rw-r--r-- 1 ec2-user ec2-user 0 Aug 10 16:45 /mnt/apps/test-jenkins.txt
This confirmed that the directory was writable.

3.Jenkins Publish Over SSH

<img width="554" height="262" alt="image" src="https://github.com/user-attachments/assets/9e46521f-1c68-4c73-8c67-187865f98211" />


The Jenkins job was configured with the Publish Over SSH plugin.
The NFS server configuration included:
Name: NFS server
Hostname: Private IP address of the NFS server
Username: ec2-user
Remote Directory: /mnt/apps
SSH private key: The .pem key used to connect to the NFS server

5.GitHub Webhook

<img width="553" height="119" alt="image" src="https://github.com/user-attachments/assets/1eda7ccd-37c3-4eb2-8a9d-91acdbc2d651" />


The Jenkins job was also configured with:
GitHub hook trigger for GITScm polling, the GitHub webhook was configured to send push events to:
http://<JENKINS_PUBLIC_IP>:8080/github-webhook/
Initially, webhook deliveries failed because the EC2 public IP address had changed. I checked the current public IP with curl http://checkip.amazonaws.com. After updating the GitHub webhook with the new IP address, the webhook successfully triggered Jenkins. A new Jenkins build, #4, was created successfully.

6.Jenkins Artifact

<img width="554" height="251" alt="image" src="https://github.com/user-attachments/assets/fffd3680-c24a-482c-8841-88146fc52d8c" />

The Jenkins job successfully checked out the GitHub repository and archived README.md. The Jenkins console output confirmed Archiving artifacts. The artifact was then sent to the NFS server using Publish Over SSH.
The successful build showed:
SSH: Connecting from host [ip-172-31-4-74]
SSH: Connecting with configuration [NFS server]
SSH: Disconnecting configuration [NFS server]
SSH: Transferred 1 file(s)
Finished: SUCCESS
The important line was SSH: Transferred 1 file(s)
This confirms that Jenkins successfully transferred the artifact.
7.Verify the Artifact on the NFS Server

<img width="554" height="267" alt="image" src="https://github.com/user-attachments/assets/8a4efa3e-4604-49a0-891b-2dee1c72f0b2" />

After the successful Jenkins build, I checked the /mnt/apps directory:
ls -l /mnt/apps the presence of README.md confirms that Jenkins successfully transferred the artifact to the NFS server. The final verification command was cat /mnt/apps/README.md. This displayed the contents of the README file that had been deployed by Jenkins.

8. Troubleshooting

<img width="554" height="118" alt="image" src="https://github.com/user-attachments/assets/f1b488ea-353e-42c7-8140-69c45992a728" />

During the configuration, I encountered several problems.
Problem 1: GitHub Webhook Failed
The GitHub webhook initially returned:
Last delivery was not successful.
failed to connect to host.
The EC2 public IP address had changed.
Solution: I checked the current public IP:
curl http://checkip.amazonaws.com
Then I updated the GitHub webhook URL with the new IP address.

Problem 2: Jenkins Crumb Error

While testing the Publish Over SSH connection, Jenkins initially displayed:
HTTP ERROR 403
No valid crumb was included in the request
After resolving the Jenkins session/crumb issue, the SSH connection test returned:
Success

Problem 3: Remote Directory Error
Jenkins initially reported:
Could not create or change to directory.
Directory [mnt]
The remote directory configuration was corrected to use:
/mnt/apps

Problem 4: Permission Denied

<img width="416" height="36" alt="image" src="https://github.com/user-attachments/assets/8f490cf6-782a-43ff-b979-a9af18773be0" />

Jenkins then reported:
ERROR: Exception when publishing, exception message [Permission denied]
I checked the ownership of /mnt/apps:
ls -ld /mnt/apps
It was owned by root:root.
I changed the ownership:
sudo chown ec2-user:ec2-user /mnt/apps
I then tested write access using:
touch /mnt/apps/test-jenkins.txt
The file was created successfully.
After running the Jenkins job again, the console showed:
SSH: Transferred 1 file(s)
Finished: SUCCESS


8.Final Result

<img width="554" height="251" alt="image" src="https://github.com/user-attachments/assets/cba0f57a-727e-4c86-83d5-9ec2c5d06a6b" />

The Jenkins-to-NFS deployment was successfully completed.
The final automated process is:
Developer
    ↓
GitHub Repository
    ↓
GitHub Webhook
    ↓
Jenkins
    ↓
Git Checkout
    ↓
Build
    ↓
Archive README.md
    ↓
Publish Over SSH
    ↓
NFS Server
    ↓
/mnt/apps/README.md
The successful Jenkins build and the presence of README.md on the NFS server confirm that the artifact deployment pipeline is working correctly.


Testing Jenkins webhook - August 10


