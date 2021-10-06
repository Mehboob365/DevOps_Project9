**TOOLING WEBSITE DEPLOYMENT AUTOMATION WITH CONTINUOUS INTEGRATION. 

 INTRODUCTION TO JENKINS**
 
**Step 1 – Install Jenkins server**

1. Create an AWS EC2 server based on Ubuntu Server 20.04 LTS and name it "Jenkins"

![image](https://user-images.githubusercontent.com/67065306/136219406-096c6220-46bb-4bef-a641-c95c8803bf47.png)


2. Install JDK (since Jenkins is a Java-based application)

     wget https://updates.jenkins-ci.org/latest/jenkins.war
     
     java -jar jenkins.war
     
     User: Admin     Password: 7a30ed3ed10e45d9a92421a46067f6b9
     
 ![image](https://user-images.githubusercontent.com/67065306/136225000-a20070ee-6370-4066-a0a4-fdcc6a3f5e24.png)


![image](https://user-images.githubusercontent.com/67065306/136225684-ba1014d8-850a-4ad7-86de-aec4fcf528c5.png)

Perform initial Jenkins setup.
From your browser access http://<Jenkins-Server-Public-IP-Address-or-Public-DNS-Name>:8080

You will be prompted to provide a default admin password

![image](https://user-images.githubusercontent.com/67065306/136225999-8cf7ec66-f392-4656-bb10-56fb33a47bbe.png)

     sudo apt update
     sudo apt install default-jdk-headless

3. Install Jenkins

    wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
    
    sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > \  /etc/apt/sources.list.d/jenkins.list'
    
    sudo apt update
    
    sudo apt-get install jenkins
    
    Make sure Jenkins is up and running

    sudo systemctl status jenkins

4. By default Jenkins server uses TCP port 8080 – open it by creating a new Inbound Rule in your EC2 Security Group

 
**Step 2 – Configure Jenkins to retrieve source codes from GitHub using Webhooks**
 
In this part, we will configure a simple Jenkins job/project (these two terms can be used interchangeably). 
This job will will be triggered by GitHub webhooks and will execute a ‘build’ task to retrieve codes from GitHub and store it locally on Jenkins server.

Enable webhooks in your GitHub repository settings
 
 
 
 
 
 
