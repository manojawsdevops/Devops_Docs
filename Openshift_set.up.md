INSTALLATIONS
Subscription-manager:
 subscription-manager is a client program that registers a system with the  Certificate-Based Red Hat Network.
Command:
    • subscription-manager status
  Reason:
       Check the status is the system registered with a valid subscription.
Command:
    • subscription-manager register
   Reason: The register command registers a new machine to the entitlement service .if not then register and provide username and password to register.
Command:
    • subscription-manager subscribe
Reason:
    •  The subscribe command allocates a specific subscription to the machine.
Command:
    • sudo yum update
Reason:
       You can use the yum update command to update applications installed on a system. If you run the command without any package names specified, it will update all packages on the system.
 

Then press Y for further continuation for updating packages








Git Installation:
Command:
    • sudo yum install git
Reason: 
   Git allows you to keep track of your code changes, revert to previous stages, work simultaneously on multiple branches, and collaborate with your fellow developers.

Then press y for installing git


After successful Installation check whether git is installed or not using bellow command.
Command:
    • git –version
      Reason:
                Checking git version.


Installion of Xvfb
Command:
    • sudo yum install Xvfb
      
Then press y for further installation



JAVA Installation:
Command:
    • sudo yum install openjdk*

Then press y for further installation


Command:
    • java -version






Jenkins Installation:
Command:
  sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo



    • sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key



    • sudo yum install Jenkins

Press Y for further installation






Command:
    • systemctl status jenkins
if Jenkins is not in active state then type below command.
    • systemctl start Jenkins

    • Then got to browser and click http://localhost:8080 then it appears like this
 

    • For administrator password goto /var/lib/Jenkins/secrets/initialAdminPassword copy the password paste in the administrator password block as shown in below.


    • click on Install suggested plugins


creating user

                             






    • click on new item and select freestyleproject and click on ok
    • In source code management selct git and paste repository url.






Docker Installation:
Command:
sudo dnf config-manager --add-repo=https://download.docker.com/linux/centos/docker-ce.repo
Reason:
 Use DNF to add and enable the official Docker CE repository.

Command:
  sudo dnf repolist -v

Command:
 dnf list docker-ce --showduplicates | sort -r
Reason:
 To list all the available docker-ce packages


Command:
     sudo dnf install docker-ce –allowerasing

Then press y for further installation




Command:
    sudo docker version




ACE Installation:
    • Move 11.0.0.7-ACE-LINUX64-DEVELOP.tar.gz to opt/ibm folder
    • Next untar 11.0.0.7-ACE-LINUX64-DEVELOP.tar.gz file
Command:
      sudo tar -xvf 11.0.0.7-ACE-LINUX64-DEVELOP.tar.gz

     After untar the file goto /opt/ibm/ace-11.0.0.7 and then type ./ace

Then type ./ace make registry global accept license silently
    
Command:
        usermod -aG mqbrkrs openshiftadmin

        usermod -aG mqbrkrs Jenkins

Next, Copy /opt/ibm/ace-11.0.0.7/server/bin/mqsiprofile to bash_profile file

Then Run . .bash_profile


OC Installation:
    • untar openshift-client-linux.tar.gz


    • move kubectl and oc to /usr/local/bin













  






