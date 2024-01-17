<h1>Ansible</h1>


<h2>Description</h2>
In this lab we installed and implemented Ansible in order to automate the setup of new a new Lamp server. This process requires two linux VMs one with ubuntu desktop and one with ubuntu server installed. For clarity purposes the ubuntu desktop will be referred to as the Ansible server, and the ubuntu server will be referred to as the ansible client.
<br />


<h2>Languages and Utilities Used</h2>

- <b>YAML</b> 
- <b>Ansible</b>

<h2>Environments Used </h2>

- <b>Ubuntu Linux</b> (22.04.1)

<h2>Process:</h2>

<br /><p align="left">
Make sure both machines are up to date and that ssh is enabled: <br/>
 - 	Sudo apt-get update
 - 	Sudo apt-get upgrade
 - 	Sudo systemctl enable ssh
<br />

Install sshpass on both machines:  <br/>
  -  Sudo apt-get install sshpass
<br />


On the client machine set the root  password for the user: <br/>
   -  Sudo passwd root
<br />


Also on the client machine allow login to root over ssh:  <br/>
   -  Sudo sed – ‘s/#PermitRootLogin prohibit-password/PermitRootLogin yes/’ etc/ssh/ssh_config
   - 	Service ssh restart
<br />


On the Ansible server install ansible:  <br/>
  -  Sudo apt-add-repository -y ppa:ansible/ansible
  -  Sudo apt-get update
  -  Sudo apt-get install -y ansible

<br />


Create and edit the ansible config file: <br/>
  -  ansible-config init --disabled > ansible.cfg
  -  copy the file to the /etc/ansible directory <br/>
    -  sudo cp ansible.cfg /etc/ansible/
  -  edit the file <br/>
    -  sudo nano /etc/ansible/ansible.cfg <br/>
    -  add the line: Host_key_checking = false in the [defaults] section

<br />


Edit the Hosts file and add the IP of the client machine to the top of the file near the comments with the other Ips then add the following lines to the bottom of the hosts file:  <br/>
  -  [all:vars] <br/>
 ansible_connection=ssh  <br/>
 ansible_ssh_user=root  <br/>
 ansible_ssh_pass=”yourPassword” *note don’t use quotes*  <br/>

 Verify that your setup is configured properly by running the following command: <br/>
  - ansible all -m ping
<br />

 If everything worked correctly you should get a message that looks like this:
<br/>
<img src="https://i.imgur.com/Ep9VfHk.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

 Now its time to create your ansible play book and save it as a yaml file. The play book I created  creates a new user named web, installs apache, installs php, installs the php ldap library, and opens port 80 on the UFW firewall. See attached file for the completed script. Once your play book is created use the command: <br/>

  -  ansible-playbook “your playbook name here”.yaml <br/>
        *note don’t use quotes* <br/>

If your playbook was done correctly your script will run and it should look like this:
 
<br/>
<img src="https://i.imgur.com/oqbfyUB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

Congrats you just automated the installation of a LAMP server!


</p>


<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
