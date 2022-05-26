# ANSIBLE REFACTORING, ASSIGNMENTS & IMPORTS

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

# Step 3: Configure UAT Webservers with a webserver role

- Launched two RHEL 8 servers named Web1-UAT and Web2-UAT
- Created a webserver role busing the following command
-```mkdir roles (in the root directory of your repo)
    cd roles
    ansible-galaxy init webserver```
 - Updated my ansible-config-mgt/inventory/uat.yml with the private IP address of the UAT webservers
 -  -  ![alt text](https://github.com/Ellawangari/DevOps-project12/blob/main/imgs/12.PNG)
 -  Edited roles/webserver/tasks/main.yml file to do the following:
  - Installed and configured Apache
  - Cloned tooling website from my GitHub repo
  - Ensured that tooling/html is deployed to /var/www/html
  - Made sure httpd service is started
    ```
    ---
    # tasks file for webserver
    - name: Install Apache and Git
      become: yes
      yum:
        name:
          - httpd
          - git
        state: present

    - name: Clone tooling app repo
      become: yes
      git:
        repo: "https://github.com/Ellawangari/tooling.git"
        dest: ~/app
        version: "HEAD"

    - name: Copy app to /var/www/html
      become: yes
      copy:
        src: ~/app/html
        dest: /var/www
        remote_src: yes
        mode: "777"
        owner: apache

    - name: Make sure httpd service is running
      become: yes
      service:
        name: httpd
        state: started
    ```
 # Step 4: Reference Webserver role
 Within static-assignments folder,I created a new file uat-webservers.yml and added the following lines
    ```
    ---
    - hosts: uat-webservers
      roles:
         - webserver
    ```
    ## and edited my site.yml like so:
    ```
    ---
    - hosts: all
    - import_playbook: ../static-assignments/common.yml

    - hosts: uat-webservers
    - import_playbook: ../static-assignments/uat-webservers.yml```
 

# Step 5: Commit and test
- Commited my changes to the refactor branch and push to GitHub, create a pull request and merge with the master branch
-  ![alt text](https://github.com/Ellawangari/DevOps-project12/blob/main/imgs/14.PNG)
- Ran the playbook against my UAT servers
 -  ![alt text](https://github.com/Ellawangari/DevOps-project12/blob/main/imgs/15.PNG)
 -  Accessed the webserver succesfully
 -   -  ![alt text](https://github.com/Ellawangari/DevOps-project12/blob/main/imgs/16.PNG)
