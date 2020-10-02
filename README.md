Ansible Role: Proxmox LXC
=========

Simplifies the creation and basic provisioning of LXC containers on [Proxmox](https://www.proxmox.com/en/) hosts.

Requirements
------------

A PVE host and desired LXC containers defined in your inventory.

Role Variables
--------------

Available variables are listed below:
```
api_host: 'orange'
api_user: 'root@pam'
```
**Required**: Specify the hostname (or IP address) and user for the target PVE host.

```
api_password: '<pve_api_password>'
ssh_pubkey: 'ssh-rsa ...'
```
The PVE password (**required**) and default SSH public key for new containers. Preferably defined in an ansible vault.

```
defaults:
  node: 'orange'
  storage: 'local-zfs'
  cores: '1'
  memory: '1024'
  disk: '3'
  onboot: yes
  pubkey: '{{ ssh_pubkey }}'
  nameserver: '1.1.1.1,8.8.8.8'
  ostemplate: 'bulk:vztmpl/centos-8-with_ssh-20200402_amd64.tar.gz'
  network: '{"net0":"name=eth0,ip=dhcp,ip6=dhcp,bridge=vmbr1"}'
```
**Required**: Your defaults for LXC containers, maybe in a group_var.

```
node: 'orange'
vmid: '240'
cores: '2'
memory: '2048'
swap: '0'
disk: '10'
onboot: yes
ostemplate: 'bulk:vztmpl/centos-8-with_ssh-20200402_amd64.tar.gz'
network: '{"net0":"name=eth0,ip=10.64.64.240/24,gw=10.64.164.1,bridge=vmbr4"}'
```
Individual host_vars file for each container.


Dependencies
------------

None.

Example Playbook
----------------
```
- name: create and start LXC container(s)
  hosts: proxmox
  gather_facts: no

  roles:
    - proxmox-lxc
```

License
-------

MIT

Author Information
------------------

This role was created in 2020 by [Raymond Douglas](https://rymnd.org).
