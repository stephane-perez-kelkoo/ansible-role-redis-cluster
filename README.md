
Ansible Role: Redis Cluster
=========

![CI](https://github.com/v0112358/ansible-role-redis-cluster/actions/workflows/main.yml/badge.svg) ![Ansible Role](https://img.shields.io/ansible/role/d/55902) [![GitHub license](https://img.shields.io/github/license/v0112358/ansible-role-redis-cluster)](https://github.com/v0112358/ansible-role-redis-cluster/blob/master/LICENSE.md)

Install and configure redis cluster on your system.

Example Inventory
------------
```
[redis_cluster:children]
redis_cluster_infra

[redis_cluster_infra]
vm-dev-redis-infra-0
vm-dev-redis-infra-1
vm-dev-redis-infra-2
vm-dev-redis-infra-3
vm-dev-redis-infra-4
vm-dev-redis-infra-5
```
Example Playbook
------------

```
---
- name: Deploy Redis Cluster
  hosts: redis_cluster
  pre_tasks:
    - name: Verify Ansible meets Redis cluster requirements.
      assert:
        that: "ansible_version.full is version_compare('2.10.0', '>=')"
        msg: >
          "You must update Ansible to at least 2.10.0 to use this playbook"
  roles:
    - { role: ansible-role-redis-cluster, tags: redis-cluster }
```

Role Variables
--------------

These variables are set in defaults/main.yml.
```
---
######### redis config
redis_cluster_replica: 1
redis_cluster_conf:
  cluster_enabled: "yes"
  port: "6379"
  maxmemory: "64mb"
  rename_commands:
    - FLUSHDB
    - FLUSHALL
    - KEYS
    - SHUTDOWN
....
```

Requirements
------------

pip packages listed in requirements.txt.

License
-------

MIT

Author Information
------------------
v0112358