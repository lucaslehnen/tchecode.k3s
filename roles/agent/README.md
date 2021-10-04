Agent role
-------------------------------------------------------------------

Configure a k3s node to be an agent node and join it on the cluster

Configure the variables
-----------------------

`server_ip` :  

The k3s server node IP;

`extra_agent_args` : 

Extra args that can be passed to the service. 
Check the k3s documentation: https://rancher.com/docs/k3s/latest/en/installation/install-options/agent-config/

Example
----------------

In your `main.yml`:

```yaml
  - hosts: agents
    roles:
        - tchecode.k3s.agent
    vars:
      server_ip: "192.168.99.11"
      extra_agent_args: ""
```
