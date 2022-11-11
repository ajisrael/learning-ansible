# Episode 1 - Introduction to Ansible

## Installing Ansible
May need to add ```--user``` to command depending on pip3 environment
```
pip3 install ansible
```
Check for correct install with
```
ansible --version
```

### Note
The following commands pertain to home lab configuration of one server on a local network.
This server's host name needed to be added to hosts file for resolution.

## First Command
### SSH Into Remote Server(s)
Make sure you can ssh into your remote server.
```
ssh ajisrael@pensieve-vm-ubu-3
```
### Create Inventory File
```
touch inventory
```
### Edit Inventory File
```
[example]
pensieve-vm-ubu-3
```
### Run First Command
Run ansible ad hoc command to ping remote server
```
ansible -i inventory example -m ping -u ajisrael
```
Should get response like the following:
```
pensieve-vm-ubu-3 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```

### Note
If you don't have ssh keys setup, you can by following the ```generate-ssh-keys.md``` doc.
Or you can add ```-K``` or ```--ask-pass``` to your command. You will then be prompted for
the password of your associated user in the request.

## Simplify Commands
### Create Ansible Configuration File
Create an ansible configuration file to specify repeated fields of your commands
```
touch ansible.cfg
```

Add parameters to configuration file: (view ```ansible.cfg``` for more details)
```
[defaults]
INVENTORY = inventory
```

### Run simplified command
```
 ansible example -m ping -u ajisrael
```
Should generate same output as before

## Other commands to try
Get free memory on remote sever(s)
```
ansible example -a "free -h" -u ajisrael
```
Get date on remote server(s)
```
ansible example -a "date" -u ajisrael
```
### Note
These previous two commands are using the default command module. So they would be the same
as running the command with ```-m command``` as well. ```-a``` refers to arguments used for
the module of the command.