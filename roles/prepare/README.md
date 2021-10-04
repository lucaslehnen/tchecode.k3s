Prepare k3s nodes
-----------------

Prepare nodes to receive k3s, downloading binary and install required packages

Configure the variables
-----------------------

`k3s_version: ` : v1.21.5+k3s1

Set the k3s version to download. 
Check available versions in: https://github.com/k3s-io/k3s/releases

Example
----------------

In your `main.yml`:

```yaml
- hosts: servers
  roles:
      - tchecode.k3s.prepare
  vars:
    k3s_version: v1.21.5+k3s1
```
