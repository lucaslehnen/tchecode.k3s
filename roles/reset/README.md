Reset k3s cluster
-----------------

Reset all changes made.

Configure the variables
-----------------------

`ansible_user` : 

Remove .kube directory for this user.

Example
----------------

In your `main.yml`:

```yaml
- hosts: servers
  roles:
      - tchecode.k3s.reset
  vars:
    ansible_user: ubuntu
```

`~ubuntu/.kube` will be removed.
