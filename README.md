# DevOps-project12

# Step 1: Jenkins Job Enhancement
- Created a new directory called ansible-config-artifact to store all artifacts after each build and changed the permissions of the file by running 
-`chmod -R 0777 /home/ubuntu/ansible-config-artifact`
-  ![alt text](https://github.com/Ellawangari/DevOps-project12/blob/main/imgs/1.PNG)
- Logged in to the Jenkins Ui console and installed the plugin Copy artifact
- ![alt text](https://github.com/Ellawangari/DevOps-project12/blob/main/imgs/2.PNG)
- Created a Freestyle project and called it save_artifacts and configure the build to be done by Ansible project(upstream project)
- ![alt text](https://github.com/Ellawangari/DevOps-project12/blob/main/imgs/3.PNG)
- ![alt text](https://github.com/Ellawangari/DevOps-project12/blob/main/imgs/4.PNG)
- ![alt text](https://github.com/Ellawangari/DevOps-project12/blob/main/imgs/5.PNG)

- Copied artifacts from other project in this case ansible project.
- ![alt text](https://github.com/Ellawangari/DevOps-project12/blob/main/imgs/6.PNG)

