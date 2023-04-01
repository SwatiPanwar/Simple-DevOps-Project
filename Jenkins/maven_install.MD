#  Install & configure Maven build tool on Jenkins
Maven is a code build tool which used to convert your code to an artifact. this is a widely used plugin to build in continuous integration


#### Prerequisites
1. Jenkins server

#### Install Maven on Jenkins
1. Download maven packages https://maven.apache.org/download.cgi onto Jenkins server. In this case, I am using /opt/maven as my installation directory
 - Link : https://maven.apache.org/download.cgi
    ```sh
     # Creating maven directory under /opt
     mkdir /opt/maven
     cd /opt/maven
     # downloading maven version 3.6.0
     wget http://mirrors.estointernet.in/apache/maven/maven-3/3.6.1/binaries/apache-maven-3.6.1-bin.tar.gz
     tar -xvzf apache-maven-3.6.1-bin.tar.gz
     ```
	
1. Setup M2_HOME and M2 paths in .bash_profile of the user and add these to the path variable
   ```sh
   vi ~/.bash_profile
   M2_HOME=/opt/maven/apache-maven-3.6.1
   M2=$M2_HOME/bin
   PATH=<Existing_PATH>:$M2_HOME:$M2
   ```
#### Checkpoint 
1. logoff and login to check maven version
  
    ```sh
    mvn --version
    ```
So far we have completed the installation of maven software to support maven plugin on the jenkins console. Let's jump onto Jenkins to complete the remaining steps. 

### Setup maven on Jenkins console
1. Install maven plugin without restart  
  - `Manage Jenkins` > `Jenkins Plugins` > `available` > `Maven Invoker`
  - `Manage Jenkins` > `Jenkins Plugins` > `available` > `Maven Integration`

2. Configure maven path
  - `Manage Jenkins` > `Global Tool Configuration` > `Maven`

for java on linux set-up JAVA_HOEM
#whereis java
#ls -l /usr/bin/java
Three Step Process: First: open Terminal->$ whereis java it would give output like this: java: /usr/bin/java /usr/share/java /usr/share/man/man1/java.1.gz

Second: ls -l /usr/bin/java It would give output like this: lrwxrwxrwx 1 root root 22 Feb  9 10:59 /usr/bin/java -> /etc/alternatives/java

Third: ls -l /etc/alternatives/java output is the JDK path: lrwxrwxrwx 1 root root 46 Feb  9 10:59 /etc/alternatives/java -> /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java
export JAVA_HOME="path that you copied"

  export PATH=$JAVA_HOME/bin:$PATH
  For all users, you have to follow below steps

sudo gedit .bashrc (for single user) FOR ALL USERS (vi /etc/profile)

export JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64/"

export PATH=$PATH:$JAVA_HOME/bin

