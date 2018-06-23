
# 'common' role

Generate the base configuration, non specific to the EVPN/VXLAN part :
 - Management Interface
 - Loopback Interface
 - Root password
 - Timezone
 - Syslog
 - User
 - SNMP
 - Static Route

Template can be found in [roles/common/templates/main.conf.j2 ](templates/main.conf.j2)

## Variables needed by the template

```yaml
loopback_ip:
global:
    root_hash:                  # Root password in Hash
    login_message:              
    time_zone:                  # Timezone
    name_servers:               # List of name servers
    ntp_servers:                # List of NTP servers
    snmp:                       # Information for SNMP
        location:
        contact:
        polling:
        - community: <community>
    routes:                     # Dict of static route to configure
        <route>: <next-hop>
```

## Example

```yaml
# File group_vars/all/common.yaml
global:
    root_hash: $1$ZUlES4dp$OUwWo1g7cLoV/aMWpHUnC/
    login_message: This is the property of Example Corp. Do not login without express permission.
    time_zone: America/Los_Angeles
    name_servers:
    - 192.168.5.68
    - 192.168.60.131
    ntp_servers:
    - 172.17.28.5
    snmp:
        location: "Site 1"
        contact: John Doe
        polling:
        - community: public
    routes:
        172.0.0.0/8: 10.94.194.254



```
