# Ansible

### Ansible Installation
Ansible is an open-source automation platform. It is very, very simple to set up and yet powerful. Ansible can help you with configuration management, application deployment, task automation.

### Pre-requisites
An AWS EC2 instance (on Control node)
Installation steps:
on Amazon EC2 instance


#### Install python and python-pip



#### Step-1:

#### Master Server :
```sh
 yum install python													sudo yum-config-manager --enable epel
													( Or)           	yum repolist
 yum install python-pip                     yum install ansible
```
### Install ansible using pip check for version
```sh
pip install ansible
ansible --version
```

### Step-2:

### Configuration Setup

1. Create a new user for ansible administration in {Master(Control server) & Slave(node server)}: #note: but same name in servers
```sh
adduser $NEW-USER-NAME
passwd  $ENTER_CUSTOM_PASSWORD
```

2. Grant admin access to user in {Master(Control server) & Slave(node server)}:
```sh
visudo 
```
Edit in file 
add this line ```sh $NEW-USER-NAME ALL=(ALL) NOPASSWD: ALL ``` and save it


3.Enable user login on all EC2 instances. (Master & Slaves)
```sh
vi /etc/ssh/sshd_config ```
set -> ```sh PasswordAuthentication yes```

			(OR)
```sh sed command replaces "PasswordAuthentication no to yes" without editing file 
		sed -ie 's/PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config		
```
#### service	sshd_config restart	 (OR) service sshd restart

#### 4. Login as $NEW-USER-NAME 	Master and generate ssh key(Master) from new session:
	
#### 5. Generate SSH Key in Master NEW USER:
	
```sh ssh-keygen ```
#### 6.	root to  cd .ssh/
#### 7. Copy SSH Key to  target servers # slave(node) servers	:
	```sh ssh-copy-id IP-ADDRESS ```
	
#### 8. Edit Host Files  #Inventory
	```sh sudo vi /etc/ansible/hosts ```
[master]
master-ip-adress
		
[slave]
node-ip-adress-1
node-ip-adress-2

#### 9. Checking from Master server

```sh ansible all -m ping ``` all servers are connecting to master
or
```sh ansible -m ping IP-ADDRESS``` specific server connecting by IP-ADDRESS
	 or
	```sh ansible -m ping master ``` master to master connection
  or
	```sh ansible -m ping slaves``` master to slaves connection
