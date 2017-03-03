# Create VM with Salt Cloud without profile files

You read everywhere (and especially [here](https://docs.saltstack.com/en/latest/topics/cloud/basic.html#creating-a-vm)) in Salt documentation that you need a profile file to create virtual machines in one of the supported clouds.

I found this approach not to be very dynamic.

It is actually not necessary to have profiles. There is a [cloud runner](https://docs.saltstack.com/en/latest/ref/runners/all/salt.runners.cloud.html), with a function `create`, dedicated to creating virtual machines. You can pass VM specifications in a pillar.

Your orchestration state `/srv/salt/states/orch_vmware/createvm.sls`:

```

Instead of using the command `salt-cloud`, we use `salt-run` like this:

```
salt-run state.orchestrate orch_vmware.createvm \ 
	pillar="{event_data: {post: {master: 'master', instances: 'vmname', \
	clonefrom: 'redhat7', datastore: 'datastore1', num_cpu: 2, memory: 4096, \
	datacenter: 'level3', cluster: 'cluster1', vlan: 'VLAN10', ip: '192.168.1.10', \
	subnet_mask: '255.255.255.0', gateway: '192.168.1.1', ssh_username: 'root', \
	password: 'example'}}}"
```