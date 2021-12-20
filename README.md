[![CI](https://github.com/de-it-krachten/ansible-role-nfs/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-nfs/actions?query=workflow%3ACI)


# ansible-role-nfs

Install NFS server/client versions v3/v4


Platforms
--------------

Supported platforms

- CentOS 7
- CentOS 8
- Debian 10 (Buster)
- Debian 11 (Bullseye)
- Ubuntu 18.04 LTS
- Ubuntu 20.04 LTS



Role Variables
--------------
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

# Use home directories located on remote NFS exports
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


Example Playbook
----------------

<pre><code>
- name: Converge
  hosts: all
  vars: null
  tasks:
    - name: Include role 'ansible-role-nfs'
      include_role:
        name: ansible-role-nfs
</pre></code>
