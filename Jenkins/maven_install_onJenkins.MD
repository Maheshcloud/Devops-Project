#  Install & configure Maven build tool on Jenkins
Maven is a code build tool which used to convert your code to an artifact. this is a widely used plugin to build in continuous integration


#### Prerequisites
1. Jenkins server

#### Install Maven on Jenkins
1. Download maven packages https://maven.apache.org/download.cgi onto Jenkins server. In this case, I am using /opt/maven as my installation directory
 - Link : https://maven.apache.org/download.cgi
    ```sh
     cd /opt
    #This example shows version 3.6.3. Substitute the download URL for the most recent version of Apache Maven from the official website. Choose the "Binary tar.gz archive".:
    sudo wget http://apache.mirrors.pair.com/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz
    #Once the download has completed, extract the downloaded archive.
    sudo tar -xvzf apache-maven-3.6.3-bin.tar.gz
    #Next, rename the extracted directory.
    sudo mv apache-maven-3.6.3 maven 
     ```
	
1. Setup M2_HOME and M2 paths in .bash_profile of the user and add these to the path variable
   ```sh
   vi ~/.bash_profile
   M2_HOME=/opt/maven
   PATH=${M2_HOME}/bin:${PATH}
   ```
#### Checkpoint 
1. logoff and login to check maven version
  
    ```sh
    mvn --version
    ```
So far we have completed the installation of maven software to support maven plugin on the jenkins console. Let's jump onto Jenkins to complete the remaining steps. 

### Setup maven on Jenkins console
1. Install maven plugin without restart  
  - `Manage Jenkins` > `Manage Plugins` > `available` > `Maven Invoker`
  - `Manage Jenkins` > `Manage Plugins` > `available` > `Maven Integration`

2. Configure maven path
  - `Manage Jenkins` > `Global Tool Configuration` > `Maven`

