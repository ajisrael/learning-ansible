# Using Vagrant

## Install Vagrant
You can download from site or use homebrew with the following command
```
brew install vagrant
```

Check install worked by checking vagrant version
```
vagrant --version
```

## Install Virtual Box
Navigate to https://www.virtualbox.org/wiki/Downloads and download and install Virtual Box.

## Generate Vagrant File
Run the following command to generate a vagrant file. This specifies the environment for your virtual machine.
```
vagrant init geerlingguy/centos7
```

## Start Virtual Machine
Start your VM by running the following command.
```
vagrant up
```

## Test Connection
Test the connection to your VM by running the following command.
```
vagrant ssh
```
To find out how to connect to your VM from a different device run the following command.
```
vagrant ssh-config
```

## Other Commands
Shutdown VM
```
vagrant halt
```
Delete VM
```
vagrant destroy
```

## Setup VM To Use Ansible
Add the following to your Vagrantfile
```
config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
end
```

Create ```playbook.yml``` file
```
touch playbook.yml
```
And then add "plays" to playbook file
```
---
- hosts: all
  become: yes
  tasks:
    - name: Ensure NTP is installed.
      yum: name=ntp state=present
    - name: Ensure NTP is running.
      service: name=ntpd state=started enabled=yes
```
This checks to make sure NTP is installed and running

## Execute Ansible Playbook On VM
Run the following command.
```
vagrant provision
```

### Note
Ansible modules help maintain idempotentcy. The first task of the play would be the same as the following task.
```
- shell: |
      if ! rpm -qa | grep -qw ntp; then
        yum install -y ntp
      fi
```
This syntax is just harder to read, but is a good example that you can run shell commands as well.