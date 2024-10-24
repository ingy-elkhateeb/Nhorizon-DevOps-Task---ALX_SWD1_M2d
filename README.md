docker build . -t name:tag
docker push name:tag 
and you are good to go ;)
docker build . -t name:tag
docker push name:tag 
and you are good to go ;)

# Project Name

This project demonstrates how to build, containerize, and automate deployment using Docker and Jenkins.

## Steps to Run the Project

### 1. Clone the Repository
First, clone the repository to your local machine</br>
### 2. Build and Run the Docker Image
sudo docker build -t your_dockerhub_username/your_image_name:latest .
### 3. Run the Docker container on port 9090
sudo docker run -d -p 9090:80 your_dockerhub_username/your_image_name:latest
Open browser and go to http://localhost:9090 to see the application running.
### 4. Push Changes to GitHub 
Make changes to your project (for example, updating the UI).
Add and commit your changes
Push your changes to GitHub
### 5. Push Docker Image to Docker Hub
log in to Docker Hub from your terminal: sudo docker login
Push the Docker image to your Docker Hub repository: sudo docker push your_dockerhub_username/your_image_name:latest 
### 6. Set Up Jenkins Pipeline
Run jenkins on a container :
sudo docker run --name jenkins \
-v /var/run/docker.sock:/var/run/docker.sock \
--privileged \
--user root \
-p 50000:5000 \
-p 8080:8080 \
-d jenkins:v1
</br>
Access Jenkins: Open Jenkins at http://localhost:8080 and complete the setup process.
Create a New Pipeline: In Jenkins, create a new pipeline project:
    Go to New Item → Pipeline, and name the project.
### 7. Create an Agent Node in Jenkins
#### Add a Jenkins Agent:

    In Jenkins, go to Manage Jenkins → Manage Nodes and Clouds → New Node.
    Configure a new node (agent) for building your project.</br>

#### Launch the Agent:

    Use either SSH or Docker-based agents to connect to Jenkins.
    Make sure the agent is up and running, and it can access your GitHub repo and Docker Hub credentials.
### 8. Set Up Jenkins Pipeline
#### create a New Pipeline:

    In Jenkins, go to New Item → Pipeline and name the project.
    Configure the pipeline script </br> 

### 9. Build and Run the Pipeline
#### Trigger the Build:

    In Jenkins, trigger the pipeline build manually or configure it to run automatically when changes are pushed to GitHub.

#### Monitor the Build:

    Watch the build process in Jenkins and make sure there are no errors during the stages (checkout, build, push, and run).
### 10. Access the Project in the Browser
Verify the Application: Once the pipeline successfully runs, go to http://localhost:9090 to see your updated project live.</br>

# *Problem we faced*
Some of us encountered issues in running jenkis file and set it up. 

1. As Example, Plugins failed to install like pipeline plugin and we're not able to find that eror on goolge (related to java)
![plugins errorp](https://github.com/user-attachments/assets/0e8189e0-e6c7-4b08-bde3-a7d7f93ac17b)
The problem was solved after the container stopped and runned again.

2. Error in connecting the second agent.
Exception in thread "main" java.nio.file.AccessDeniedException: /home/jenkins/agent4
	at java.base/sun.nio.fs.UnixException.translateToIOException(UnixException.java:90)
	at java.base/sun.nio.fs.UnixException.rethrowAsIOException(UnixException.java:111)
	at java.base/sun.nio.fs.UnixException.rethrowAsIOException(UnixException.java:116)
	at java.base/sun.nio.fs.UnixFileSystemProvider.createDirectory(UnixFileSystemProvider.java:389)
	at java.base/java.nio.file.Files.createDirectory(Files.java:690)
	at java.base/java.nio.file.Files.createAndCheckIsDirectory(Files.java:797)
	at java.base/java.nio.file.Files.createDirectories(Files.java:783)
	at org.jenkinsci.remoting.engine.WorkDirManager.initializeWorkDir(WorkDirManager.java:211)
	at hudson.remoting.Launcher.initialize(Launcher.java:465)
	at hudson.remoting.Launcher.run(Launcher.java:444)
	at hudson.remoting.Launcher.main(Launcher.java:416)

unfortunately, we're unable to solve this issue yet. we ran this command for connecting the agent 

curl -sO http://localhost:8080/jnlpJars/agent.jar
java -jar agent.jar -url http://localhost:8080/ -secret e386acf59667395a7b8f86b69fd65ba282df6fb90d3e0b32e55f2cb7c057bcc6 -name Agent4 -workDir "/home/jenkins/agent4"
Exception in thread "main" java.nio.file.AccessDeniedException: /home/jenkins/agent4

3. Using compose file we encountered an error 


