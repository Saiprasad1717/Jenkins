1) Update the package list to ensure you have the latest package versions:
sudo apt update
sudo apt upgrade -y


2) Jenkins requires Java to run. Install OpenJDK 11:
sudo apt install openjdk-11-jdk -y


3) Add the Jenkins Debian package repository to your system and import its GPG key:

curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

4) Install Jenkins
     sudo apt update
     sudo apt install jenkins -y

5) Start the Jenkins service and enable it to start on boot:
sudo systemctl start jenkins
sudo systemctl enable jenkins


#Open Port 8080 on EC2 Security Group
Jenkins runs on port 8080 by default. You need to open this port in your EC2 security group:

1)Go to the AWS Management Console.
2)Navigate to "EC2" > "Instances".
3)Select your EC2 instance and click on "Security Groups" in the lower panel.
4)Click on "Edit inbound rules".
5) Add a rule with:
     Type: Custom TCP
     Port Range: 8080
     Source: 0.0.0.0/0 (or restrict to your IP address for security)

6)  Complete Jenkins Setup
   You will be prompted for an initial admin password. Retrieve it by running
sudo cat /var/lib/jenkins/secrets/initialAdminPassword


