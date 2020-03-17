# Ansible

### Ansible Installation
Ansible is an open-source automation platform. It is very, very simple to set up and yet powerful. Ansible can help you with configuration management, application deployment, task automation.

### Pre-requisites
An AWS EC2 Ubuntu instance (MAster or Control node)


#### Step-1: 

##### Install ansible on Master Server :
```sh
sudo apt update
sudo apt install software-properties-common
sudo apt-add-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
```


#### Step-2:

##### Configuration Setup

1. Create a new user for ansible administration in {Master(Control server) & Slave(node server)} #note: but same name in servers
```sh
adduser $NEW-USER-NAME
passwd  $ENTER_CUSTOM_PASSWORD
```

2. Grant admin access to user in {Master(Control server) & Slave(node server)}:
```sh
visudo 
```
Edit and add below line to file 
```sh 
$NEW-USER-NAME ALL=(ALL) NOPASSWD: ALL 
```

3.Enable user login on all EC2 instances. (Master & Slaves)
```sh
vi /etc/ssh/sshd_config
```
set ->  
```sh 
PasswordAuthentication yes
```
(OR)
```sh 
sed command replaces "PasswordAuthentication no to yes" without editing file
sed -ie 's/PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config		
```
#### service	sshd_config restart	 (OR) service sshd restart

#### 4. Login as $NEW-USER-NAME 	Master and generate ssh key(Master) from new session:
	
#### 5. Generate SSH Key in Master NEW USER:
```sh 
ssh-keygen 
```
#### 6.	root to  cd .ssh/
#### 7. Copy SSH Key to  target servers # slave(node) servers	:
```sh 
ssh-copy-id IP-ADDRESS 
```
#### 8. Edit Host Files  #Inventory
```sh 
sudo vi /etc/ansible/hosts 
```
##### [master]
master-ip-adress
		
##### [slave]
node-ip-adress-1
node-ip-adress-2

#### 9. Checking from Master server
1. All servers are connecting to master
```sh 
ansible all -m ping 
```

2. specific server connecting by IP-ADDRESS
```sh 
ansible -m ping IP-ADDRESS
```

3. master to master connection
```sh 
ansible -m ping master 
``` 

4. master to slaves connection
```sh
ansible -m ping slaves
```
