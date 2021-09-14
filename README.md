Keycloak HA Cluster
=========

Simple ansible role for deploying Keycloak HA Cluster

Requirements
------------

CentOS 7/8 with started Firewalld service
The role contains self-signed SSL certificate (./files/). Feel free to replace it with your own.

Role Variables
--------------

See [defaults/main.yml](defaults/main.yml)

Dependencies
------------

```yml
- role: andrewrothstein.etcd-cluster
  version: v2.0.0
- role: kostiantyn-nemchenko.patroni
  version: v1.2.0
```

Example Playbook
----------------
Inventory:
```ini
[keycloak]
192.168.1.2 ansible_user=root keepalived_state=MASTER keepalived_priority=100
192.168.1.3 ansible_user=root keepalived_state=BACKUP keepalived_priority=90
192.168.1.4 ansible_user=root keepalived_state=BACKUP keepalived_priority=80
```

Playbook:
```yml
- hosts: keycloak
  become: yes
  roles:
    - role: scorsair.keycloak-ha-cluster
      keycloak.keepalived.virtual_ip: "192.168.1.5"
```

License
-------

MIT

Author Information
------------------

Stanislav Garifullin <corsair.home@gmail.com>
