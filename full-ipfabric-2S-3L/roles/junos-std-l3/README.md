

# Description



## Variables

```yaml
junos-std-l3:
    - name: xe-0/0/0
      units:
      - id: 0
        ip: 192.168.1.10
        mask: 24
    - name: xe-0/0/1
      vlan_tagging: vlan-tagging
      units:
      - id: 2
        vlan_id: 20
        ip: 192.168.1.10
        mask: 24
```
