# role openvpn
This role does the configuration of the OpenVPNServer.


## Variables
### Default
Some variables are already defined in defaults/main.yml


| Variable       | Description                   | Default value |
|----------------|-------------------------------|---------------|
| `openvpn_easyrsa_url`     | URL to download EasyRSA         | `https://github.com/OpenVPN/easy-rsa/releases/download/v{{openvpn_easyrsa_version }}/EasyRSA-{{ openvpn_easyrsa_version }}.tgz`      |
| `openvpn_easyrsa_dest`        | Directory to install EasyRSA           | `/home/openvpn`      |
| `openvpn_home`  | home directory of openvpn      | `/home/openvpn`     |
| `openvpn_easyrsa_server_name`  | Name of OpenVPN      | `server`     |
| `openvpn_port`  | Port of OpenVPN      | `1194`     |
| `openvpn_protocol`  | Protocol of OpenVPN      | `udp`     |

### Other
Put these variables e.g. in the file host_vars or group_vars

#### EasyRSA CA
| Variable       | Description                   |
|----------------|-------------------------------|
| `openvpn_easyrsa_version`  | Version of EasyRSA      |
| `openvpn_easyrsa_country`  | Country code for EasyRSA CA      |
| `openvpn_easyrsa_province`  | Province for EasyRSA CA      |
| `openvpn_easyrsa_city`  | City for EasyRSA CA      |
| `openvpn_easyrsa_org`  | Organisation for EasyRSA CA      |
| `openvpn_easyrsa_email`  | Email for EasyRSA CA      |
| `openvpn_easyrsa_ou`  | Organisation Unit for EasyRSA CA      |
| `openvpn_easyrsa_common_name`  | Common name for EasyRSA CA      |

#### Client name
| Variable       | Description                   |
|----------------|-------------------------------|
| `openvpn_client_name`  | Client name for OpenVPN      |


#### OpenVPN Client configuration
Example:
```
openvpn_client_conf_lines:
  - {regexp: '^remote\s+.*',
      line: "remote {{ ansible_facts['default_ipv4']['address'] }} {{ openvpn_port }}"}
  - {regexp: '^proto\s+\w+(?:\s+#.*)?$',
      line: 'proto {{ openvpn_protocol }}'}
  - {regexp: '^;user.*$', line: 'user nobody'}
  - {regexp: '^;group.*$', line: 'group nogroup'}
  - {regexp: '^ca ca.cert', line: '#ca ca.cert'}
  - {regexp: '^cert client.cert', line: '#cert client.cert'}
  - {regexp: '^key client.key', line: '#key client.key'}
  - {regexp: '^;?tls-auth ta\.key 1(?:\s+#.*)?$',
     line: 'tls-auth ta.key 1 # This file is secret'}
```

#### OpenVPN Server configuration
Example:
```
openvpn_server_conf_lines:
  - {regexp: '^;?tls-auth ta\.key 0(?:\s+#.*)?$',
     line: 'tls-auth ta.key 0 # This file is secret'}
  - {regexp: '^;user.*$', line: 'user nobody'}
  - {regexp: '^;group.*$', line: 'group nogroup'}
  - {regexp: '^;push "redirect-gateway\s+',
     line: 'push "redirect-gateway def1 bypass-dhcp"'}
```
