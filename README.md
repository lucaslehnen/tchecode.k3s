# Ansible Collection - tchecode.k3s

It's an Ansible collection with roles to install a k3s cluster.
Supports arm64 and amd64 hosts running Ubuntu OS.

## How to use

Define your inventory in `hosts` file:
```
[k3s_server]
192.168.99.21
192.168.99.22
192.168.99.23

[k3s_agent]
192.168.99.24
192.168.99.25
192.168.99.26
192.168.99.27

[k3s_cluster:children]
k3s_server
k3s_agent
```

Create your playbook `site.yml`:

```YAML
- hosts: k3s_cluster
  user: ubuntu
  become: true
  gather_facts: true
  roles:
    - {role: commom, tags: [k3s]}
  vars:
    k3s_version: v1.21.5+k3s1

- hosts: k3s_server
  user: ubuntu
  become: true
  gather_facts: false
  roles:
    - {role: config-server, tags: [k3s]}    
  vars:
    server_ip: "{{ hostvars[groups['k3s_server'][0]]['ansible_host'] | default(groups['k3s_server'][0]) }}"
    ansible_user: ubuntu
    extra_server_args: "--write-kubeconfig-mode 644"

- hosts: k3s_agent
  user: ubuntu
  become: true
  gather_facts: false
  roles:
    - {role: k3s-config-worker, tags: [k3s]}
  vars:
    server_ip: "{{ hostvars[groups['k3s_server'][0]]['ansible_host'] | default(groups['k3s_server'][0]) }}"
    extra_agent_args: ""
```

Run the playbook:

```
ansible-playbook -i hosts site.yml
```

To revert all changes, you can call the role `reset`. I Suggest another playbook, `reset.yml` for example:

```YAML
- hosts: k3s_cluster
  user: ubuntu
  become: true
  roles:
    - {role: k3s-reset, tags: [reset]}
  vars:
    ansible_user: ubuntu
```
