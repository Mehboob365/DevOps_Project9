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

 
 ![image](https://user-images.githubusercontent.com/67065306/136272944-44eb794b-6a92-4b41-8852-c51bcce99679.png)

 ![image](https://user-images.githubusercontent.com/67065306/136274892-90fce32a-1330-4053-b5f4-463fe7f08395.png)

 ![image](https://user-images.githubusercontent.com/67065306/136274956-02de72f1-de52-4b46-a191-2d750a9bf74b.png)

 Now, we will go ahead and make some change in any file in your GitHub repository (e.g. README.MD file) and push
 the changes to the master branch. We will see that a new build has been launched automatically (by webhook) and 
 we can see its results – artifacts, saved on Jenkins server as below.

 ![image](https://user-images.githubusercontent.com/67065306/136277364-a1a58f2a-8045-49d3-b887-fac23ae8f373.png)

We have now configured an automated Jenkins job that receives files from GitHub by webhook trigger (this method is 
considered as ‘push’ because the changes are being ‘pushed’ and files transfer is initiated by GitHub). 
There are also other methods: trigger one job (downstreadm) from another (upstream), poll GitHub periodically and others.

By default, the artifacts are stored on Jenkins server locally

ls /var/lib/jenkins/jobs/tooling_github/builds/<build_number>/archive/
 
**CONFIGURE JENKINS TO COPY FILES TO NFS SERVER VIA SSH**
 
Step 3 – Configure Jenkins to copy files to NFS server via SSH

 Now we have our artifacts saved locally on Jenkins server, the next step is to copy them to our NFS server to /mnt/apps directory.

Jenkins is a highly extendable application and there are 1400+ plugins available. 
 
We will need a plugin that is called "Publish Over SSH".
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
