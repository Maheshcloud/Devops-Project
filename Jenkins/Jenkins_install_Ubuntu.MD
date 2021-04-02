
# Install Jenkins on AWS Ubuntu 18 EC2 instance
Jenkins is a self-contained Java-based program, ready to run out-of-the-box, with packages for Windows, Mac OS X and other Unix-like operating systems. As an extensible automation server, Jenkins can be used as a simple CI server or turned into the continuous delivery hub for any project.


### Prerequisites
AWS Security Group:
Need to Open port 22 for SSH, port 80 for HTTP and port 443 for HTTPS and port 8080 as Jenkins runs on port 8080


## Install Java
1. We will be using open java for our demo, Get the latest version from http://openjdk.java.net/install/
   ```sh
   sudo add-apt-repository ppa:openjdk-r/ppa
   sudo apt-get update
   sudo apt install openjdk-11-jdk
  
   ```

1. Confirm Java Version and set the java home
   ```sh
   java -version
   pathofjava=$(find /usr/lib/jvm/java-* | head -n 1)
   export JAVA_HOME=$pathofjava
   export PATH=$JAVA_HOME/bin:$PATH
  
   _The output should be something like this,_
    ```sh
   [root@~]# java -version
   openjdk version "11.0.10" 2021-01-19
   OpenJDK Runtime Environment (build 11.0.10+9-Ubuntu-0ubuntu1.18.04)
   OpenJDK 64-Bit Server VM (build 11.0.10+9-Ubuntu-0ubuntu1.18.04, mixed mode, sharing)
   ```

## Install Jenkins
 You can install jenkins using the rpm or by setting up the repo. We will set up the repo so that we can update it easily in the future.
1. Get the latest version of jenkins from https://pkg.jenkins.io/redhat-stable/ and install
   ```sh
   wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
   sudo sh -c 'echo deb http://pkg.jenkins-ci.org/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
   sudo apt -y update
   sudo apt install -y jenkins
   ```

   ### Start Jenkins
   ```sh
   # Start jenkins service
   service jenkins start
   
   # Check the Status of Jenkins
   service jenkins status
   
   If status of jenkins is  Active: active (exited), then perform below steps:
   sudo ufw allow 8080
   sudo ufw allow OpenSSH
   sudo ufw enable

   # Setup Jenkins to start at boot,
   chkconfig jenkins on
   ```

   ### Accessing Jenkins
   By default jenkins runs at port `8080`, You can access jenkins at
   ```sh
   http://YOUR-SERVER-PUBLIC-IP:8080
   ```
  #### Configure Jenkins
- The default Username is `admin`
- Grab the default password 
- Password Location:`/var/lib/jenkins/secrets/initialAdminPassword`

- Change admin password
   - `Admin` > `Configure` > `Password`
- Configure `java` path
  - `Manage Jenkins` > `Global Tool Configuration` > `JDK`  
- Create another admin user id

### Test Jenkins Jobs
1. Create “new item”
1. Enter an item name – `My-First-Project`
   - Chose `Freestyle` project
1. Under the Build section
	Execute shell: echo "Welcome to Jenkins"
1. Save your job 
1. Build job
1. Check "console output"
install java 
