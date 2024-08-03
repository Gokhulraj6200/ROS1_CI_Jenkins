// Powered by Infostretch 

timestamps {

node () {

	stage ('ros1_ci_test - Checkout') {
 	 checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '363726ec-b770-45ab-a0f6-47832ec017d1', url: 'git@github.com:Gokhulraj6200/ROS1_CI_Jenkins.git']]]) 
	}
	stage ('ros1_ci_test - Build') {
 			// Shell build step
sh """ 
source /opt/ros/noetic/setup.bash
mkdir -p ~/ros_jenkins_ws/src
cd ~/ros_jenkins_ws
# Running catkin_make the first time will create a CMakeLists.txt file inside the 'src' folder
catkin_make 
 """		// Shell build step
sh """ 
#!/bin/bash
cd /home/user/ros_jenkins_ws/src
echo "Will check if we need to clone or just pull"
if [ ! -d "ROS1_CI_Jenkins" ]; then
  git clone https://github.com/Gokhulraj6200/ROS1_CI_Jenkins.git
else
  cd ROS1_CI_Jenkins
  git pull origin main
fi 
 """		// Shell build step
sh """ 
cd ~/ros_jenkins_ws
sudo apt-get update
sudo apt-get install -y docker.io docker-compose
sudo service docker start
sudo usermod -aG docker $USER
newgrp docker 
 """		// Shell build step
sh """ 
cd ~/ros_jenkins_ws/src/ROS1_CI_Jenkins
sudo docker build -t tortoisebot-ros1-test:latest . 
 """		// Shell build step
sh """ 
cd ~/ros_jenkins_ws/src/ROS1_CI_Jenkins
sudo docker run --net=bridge -e DISPLAY -e ROS_MASTER_URI=http://localhost:11311 -e ROS_HOSTNAME=localhost -v /tmp/.X11-unix:/tmp/.X11-unix tortoisebot-ros1-test 
 """ 
	}
}
}