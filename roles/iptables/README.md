# Configuration of the iptables

## Variables

put these variables e.g. in the file ../host_vars/FQDN-HOSTNAME or ../group_vars/all
```
iptables_rules:
  - comment: "Allow smtp port 25"
    chain: INPUT
    destination_port: '25'
    jump: ACCEPT
    protocol: tcp
```
