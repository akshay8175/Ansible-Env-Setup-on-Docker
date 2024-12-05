# Ansible Setup in Docker containers.
---------------------
### Step 1. Install docker in your system (Linux and Windows ) and check version 
> docker version
--------------------
### Step 2. Create docker image (Ubuntu)
  > docker pull ubuntu
  > docker images
---------------------
# Step 3. Create Docker container 
  > docker run -itd --name ansible_master ubuntu /bin/bash
  > docker run -itd --name normalos ubuntu /bin/bash
-----------------------
### Step 4. Check the docker images using below command
  > docker ps -a
------------------------
### Step 5. Using below command attach each container and access ubuntu terminal.
  > docker attach `container-id`
-------------------------
### Steps 6. Install some initial packages in the both dockers machines.
  > apt update; apt install ssh vim net-tools -y
  > apt install python ansible openssh-client vim iputils -ping -y
------------------------
### Steps 7. After installed packages... set the root user password in 'normalOS' docker container.
  > passwd root
-------------------------
### Step 8. Change the ssh configuration in 'normalOS' docker container.
  > vim /etc/ssh/sshd_config
  ![image](https://github.com/user-attachments/assets/0c57c800-f10e-4220-ac29-13b791b9cd38)
--------------------------
### Step 9. After `permitrootlogin yes` restart the ssh service using below command
  > service ssh restart
-------------------------
### Step 10. Check the ip address of both docker container ubuntu machines.
  > docker network inspect bridge
!!! Note: Use above command after start the docker containers...
------------------------------------
### Step 11. After check the both machines ip address 
. ping to normalos from ansible master
  > ping 172.17.0.3
----------------------------
### Step 12. after success connected both machines...
- generate the ssh keygen using below command
  > ssh-keygen
  > ssh-copy-id root@172.17.0.3
  > ssh root@172.17.0.3
--------------------------
### Step 13. Create and hosts file using below command.
  > vi /etc/ansible/hosts          (golbal hosts file for ansible)
  > vi /ansible/hosts
---------------------------
### Step 14. Check the ansible is success ping to target machine(172.17.0.3) or not?
  > ansible hosts -m ping        (command use for global ansible hosts)
  > ansible test -i hosts -m ping
-----------------------------
### Step 15. First ansible playbook..
```yml
- name: My first play
  hosts: hosts
  tasks:
   - name: Ping my hosts
     ansible.builtin.ping:

   - name: Print message
     ansible.builtin.debug:
       msg: Hello world

```
