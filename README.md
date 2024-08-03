# ROS1_CI_Jenkins

# ROS Noetic

# Jenkins Setup for ROS1 CI for Tortoisebot waypoint server test

This guide is for setting up Jenkins for Continuous Integration in the `ros1_ci` repository.

## Follow the steps below

#### set the environment to noetic
```bash
source ~/simulation_ws/devel/setup.bash
```

#### Install and Start Docker in the Server
```bash
sudo apt-get update
sudo apt-get install -y docker.io docker-compose
sudo service docker start
```
#### Before starting jenkins check for ssh permission 

```bash
git ls-remote -h -- git@github.com:Gokhulraj6200/ROS1_CI_Jenkins.git HEAD
```
if the above command does nothing then skip to next step, if its asks for permission, then enter yes, like below

```bash
The authenticity of host 'github.com (4.208.26.197)' can't be established.
ECDSA key fingerprint is SHA256:xxxxxxxxxxxxxxxxx/R1BUFWu3/LiyKgUfQM.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
```

#### After setting git authorization, start the jenkins using following commands

```bash
cd ~/webpage_ws
bash start_jenkins.sh
cat /home/user/jenkins__pid__url.txt
```

#### follow the Jenkins url link, and login using the credentials

- User: admin
- Password: gokhul123

#### Build CI Test Manually in Jenkins

##### Here we have two projects for ros1 testing, follow the instructions below for further understanding

- ros1_ci_test-Pipeline

This project follows pipeline syntax, to build  this project manually go to the project and press "Build Now" button

#### Mulitbuild trigger

- ros1_ci_test 

This project is configured using freestyle method, to build this project manually go to the project and press "Build Now" button, when building it, triggers the ros1_ci_test-Pipeline and that project is queued and once the ros1_ci_test project is built the ros1_ci_test-pipeline project aslo builds..

##### Note: 

- Both the projects start the same docker image and so the same test, this is just to experiment and learn new plugins available.

#### Build CI Test by commit trigger request

- we can automate the build process whenever we modify and commit changes to the github account.
- Create a pull request and and once the changes are made then we can see the project is build.
- we can also confirm it by navigating to console output and check that the build has been triggered with SCM.

##### Note:

- this method takes time to build the project