[![CI](https://github.com/de-it-krachten/ansible-role-nfs/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-nfs/actions?query=workflow%3ACI)


# ansible-role-nfs

Install NFS server/client versions v3/v4



## Dependencies

#### Roles
None

#### Collections
- community.general
- ansible.posix

## Platforms

Supported platforms

- Red Hat Enterprise Linux 7<sup>1</sup>
- Red Hat Enterprise Linux 8<sup>1</sup>
- Red Hat Enterprise Linux 9<sup>1</sup>
- CentOS 7
- RockyLinux 8
- RockyLinux 9
- OracleLinux 8
- AlmaLinux 8
- AlmaLinux 9
- Debian 11 (Bullseye)
- Ubuntu 20.04 LTS
- Ubuntu 22.04 LTS
- Fedora 35
- Fedora 36

Note:
<sup>1</sup> : no automated testing is performed on these platforms

## Role Variables
### defaults/main.yml
<pre><code>
# Install/confire NFS server
nfs_server: false

# Install/confire NFS client
nfs_client: true

# Configure NFS to use KRB5 (kerberos)
nfs_krb5: false

# Open firewall ports
nfs_firewall: true

# List of NFS mount
nfs_mounts: []

# Enable the use of home directories located on remote NFS exports
# This will set the appropiate SELinux boolean
nfs_home_dir: false

# NFS implementation(s) to use
nfs_v3: false
nfs_v4: true

# Ports to use to make NFS v4 work thgrough firewall
nfs_statd_port: "32766"
nfs_mountd_port: "32767"
nfs_lockd_port: "32768"

# List of NFS v3 ports
nfs_v3_server_firewall_ports:
  - port: '2049'
    proto: tcp
  - port: '111'
    proto: tcp
  - port: '111'
    proto: udp
  - port: "{{ nfs_statd_port }}"
    proto: tcp
  - port: "{{ nfs_statd_port }}"
    proto: udp
  - port: "{{ nfs_mountd_port }}"
    proto: tcp
  - port: "{{ nfs_mountd_port }}"
    proto: udp
  - port: "{{ nfs_lockd_port }}"
    proto: tcp
  - port: "{{ nfs_lockd_port }}"
    proto: udp

# List of NFS v4 ports
nfs_v4_server_firewall_ports:
  - port: '2049'
    proto: tcp
</pre></code>


### vars/family-RedHat.yml
<pre><code>
# Server packages
nfs_server_packages:
  - nfs-utils

# Server packages for kerberos support
nfs_server_packages_krb5:
  - gssproxy

# Client packages
nfs_client_packages:
  - nfs-utils

# Server services
nfs_server_services:
  - rpcbind
  - nfs-server

# Server services for kerberos support
nfs_server_services_krb5:
  - gssproxy
  - rpc-gssd

# Client services for kerberos support
nfs_client_services_krb5:
  - gssproxy
  - rpc-gssd
</pre></code>

### vars/family-Debian.yml
<pre><code>
# Server packages
nfs_server_packages:
  - nfs-kernel-server
  - procps

# Server packages for kerberos support
nfs_server_packages_krb5:
  - gssproxy

# Client packages
nfs_client_packages:
  - nfs-common

# Server services
nfs_server_services:
  - nfs-kernel-server

# Server services for kerberos support
nfs_server_services_krb5:
  - rpc-gssd

# Client services for kerberos support
nfs_client_services_krb5:
  - rpc-gssd
</pre></code>



## Example Playbook
### molecule/default/converge.yml
<pre><code>
- name: sample playbook for role 'nfs'
  hosts: all
  become: "{{ molecule['converge']['become'] | default('yes') }}"
  tasks:
    - name: Include role 'nfs'
      ansible.builtin.include_role:
        name: nfs
</pre></code>
