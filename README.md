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

- Tested my setup by editing the readme file to automatically configured a build from jenkins.
- ![alt text](https://github.com/Ellawangari/DevOps-project12/blob/main/imgs/7.PNG)
- ![alt text](https://github.com/Ellawangari/DevOps-project12/blob/main/imgs/8.PNG)

# Step 2: Refactor Ansible Code
- Pulled the new code from GitHub, created and checkout to a new branch named refactor
    ```git pull origin master
        git checkout -b refactor```
        
 - ![alt text](https://github.com/Ellawangari/DevOps-project12/blob/main/imgs/9.PNG)
 - Within playbooks folder, I  created site.yml file  which would serve as my primary playbook.
 - Created a folder called static-assignments and moved the common.yml file to the created folder.
 - Inside site.yml file, I  imported the  common.yml playbook
 - ![alt text](https://github.com/Ellawangari/DevOps-project12/blob/main/imgs/9.PNG)
 - Ran the ansible playbook command using the dev environment using this command 
 - `ansible-playbook -i /home/ubuntu/ansible-config-mgt/inventory/dev.yml /home/ubuntu/ansible-config-mgt/playbooks/site.yaml`
 - ![alt text](https://github.com/Ellawangari/DevOps-project12/blob/main/imgs/10.PNG)
 -  Once the playbook completed succesfully checked the webservers to ensure wireshark was installled succesfully.
 -  ![alt text](https://github.com/Ellawangari/DevOps-project12/blob/main/imgs/11.PNG)

