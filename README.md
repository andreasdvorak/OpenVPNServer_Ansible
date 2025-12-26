# Introduction
Installation of an OpenVPNServer with Ansible

# Requirements
You need a Linux server.

# Prepation
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

[local]
localhost ansible_connection=local

```
