# ngpaas-monitoring-roles-poc

## Synopsis
This repository is a Proof of Concept (PoC) for the NGPaaS monitoring stack deploy.

## Getting started

### Prerequisites
* Ansible 2.4.x
* python 2.7.x

### How to execute
This PoC is targeted for Cloud GARR. The infrastructure consists of 4 Debian9 nodes. One of them acts as a bastion and it is available on the public network.
A valid ssh config can the following one:

```
# ngpaas-test
Host ngpaas-test-node-1
    Hostname node.public.ip
    User root
    IdentityFile ~/.ssh/ngpaas-test.pem

Host ngpaas-test-node-2
    Hostname node.local.ip
    User root
    ProxyCommand ssh ngpaas-test-node-1 nc %h %p
    IdentityFile ~/.ssh/ngpaas-test.pem

Host ngpaas-test-node-3
    Hostname node.local.ip
    User root
    ProxyCommand ssh ngpaas-test-node-1 nc %h %p
    IdentityFile ~/.ssh/ngpaas-test.pem

Host ngpaas-test-node-4
    Hostname node.local.ip
    User root
    ProxyCommand ssh ngpaas-test-node-1 nc %h %p
    IdentityFile ~/.ssh/ngpaas-test.pem
```

Since Cloud GARR fresh VMs disallow to connect using root, the `init-os` playbook has to be executed with the following command:

```
$ ansible-playbook -i inventory -u debian -b init-vm.yml
```
The base role will change that behaviour.

Then, the `monitoring-example-stack` playbook can be executed with the following command:

```
$ ansible-playbook -i inventory monitoring-example-stack.yml
```

## License
This project is licensed under the AGPLv3. See the [LICENSE.md](LICENSE.md) file for details.