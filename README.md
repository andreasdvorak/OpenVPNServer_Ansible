# Introduction
Installation of an OpenVPNServer with Ansible

# Requirements
You need a Linux server.

# Prepation
## User ansible
You need the user ansible to run Ansible.
```
groupadd -g 300 ansible
useradd -c "Ansible" -d /home/ansible -g ansible -m -s /bin/bash -u 300 ansible
mkdir /home/ansible/.ssh
echo "<public_key>" > /home/ansible/.ssh/authorized_keys
chown -R ansible:ansible /home/ansible/.ssh
chmod 700 /home/ansible/.ssh
chmod 600 /home/ansible/.ssh/authorized_keys
echo "ansible ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/ansible
```

## Python
create a virtual environment
```
pip3 install virtualenv
```

create a virtual environment
```
virtualenv -p python3 env
```
The result is the folder "env"

activation of virtual environment
```
. env/bin/activate
```

### Python requirements
install the requirements on the destination host
```
python -m pip install -r requirements.txt
```

## Ansible
Installation of Azure collection, but it should be installed by default.
## Inventory
Create these directorys and files

You need at least this file with the content below.
```
inventory/hosts.ini

[openvpn]

[all:vars]
ansible_user=ansible
ansible_ssh_private_key_file=
```

## First tests
### Show inventory
Show hosts form inventory
```
ansible-inventory --list
```
### Connection test
Check connection to hosts
```
ansible all -m ping
```
## Show facts
Show facts of "all" server.
```
ansible all -m setup
```
## Ansible run
Run Ansible with playbook openvpn
```
ansible-playbook playbooks/openvpn.yml
```

test the playbook
```
--check
```

show difference
```
--diff
```

limit execution to a certain host
```
--limit openvpn
```
