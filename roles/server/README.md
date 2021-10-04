Configure K3s server 
-----------------------

This role install, configure and start k3s server. 

Configure the variables
-----------------------

`server_ip` :  

The k3s server node IP;

`extra_server_args` : 

Extra args that can be passed to the service. 
Check the k3s documentation: https://rancher.com/docs/k3s/latest/en/installation/install-options/server-config/

`ansible_user` : 

User to configure access to Kubernetes cluster via CLI/kubectl

Example
----------------

In your `main.yml`:

```yaml
- hosts: k3s-servers
  roles:
      - tchecode.k3s.server
  vars:
    server_ip: "192.168.99.11"
    ansible_user: ubuntu
    extra_server_args: "--write-kubeconfig-mode 644"
```
