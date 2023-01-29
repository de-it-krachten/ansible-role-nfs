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
- OracleLinux 9
- AlmaLinux 8
- AlmaLinux 9
- Debian 11 (Bullseye)
- Ubuntu 20.04 LTS
- Fedora 36
- Fedora 37

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

# Exclude this mount if this string is found in the source name/ip
nfs_mount_exclude: DUMMY

# Enable the use of home directories located on remote NFS exports
# This will set the appropiate SELinux boolean
nfs_home_dir: false

# NFS implementation(s) to use
nfs_v3: false
nfs_v4: true

# Ports to use to make NFS v3 work through firewall
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

### defaults/family-Debian.yml
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

# Exclude this mount if this string is found in the source name/ip
nfs_mount_exclude: DUMMY

# Enable the use of home directories located on remote NFS exports
# This will set the appropiate SELinux boolean
nfs_home_dir: false

# NFS implementation(s) to use
nfs_v3: false
nfs_v4: true

# Ports to use to make NFS v3 work through firewall
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
    proto: 'tcp'

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

### defaults/family-RedHat.yml
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

# Exclude this mount if this string is found in the source name/ip
nfs_mount_exclude: DUMMY

# Enable the use of home directories located on remote NFS exports
# This will set the appropiate SELinux boolean
nfs_home_dir: false

# NFS implementation(s) to use
nfs_v3: false
nfs_v4: true

# Ports to use to make NFS v3 work through firewall
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
  - service: 'nfs'
    proto: tcp
  - service: 'mountd'
    proto: tcp
  - service: 'rpc-bind'
    proto: tcp

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




## Example Playbook
### molecule/default/converge.yml
<pre><code>
- name: sample playbook for role 'nfs'
  hosts: all
  become: true
  tasks:

- name: sample playbook for role 'nfs'
  hosts: nfs_servers
  become: true
  vars:
    # nfs_v3: true
    # nfs_v4: false
    nfs_v3: false
    nfs_v4: true
    __nfs_server: "{{ groups['nfs_servers'] | first }}"
    __nfs_client: "{{ groups['nfs_clients'] | first }}"
    export_path: /export/test
    clients: "{{ [ ( inventory_hostname | regex_replace('-server', '-client')) ] }}"
  tasks:

    - name: Create path to export
      ansible.builtin.file:
        path: "{{ export_path }}"
        state: directory
        mode: "0755"

    - name: Setup NFS server
      ansible.builtin.include_role:
        name: nfs
      vars:
        nfs_server: true
        nfs_exports:
          - { path: "{{ export_path }}", clients: "{{ clients }}", options: 'rw,sync,no_root_squash' }

- name: sample playbook for role 'nfs'
  hosts: nfs_clients
  become: true
  vars:
    # nfs_v3: true
    # nfs_v4: false
    nfs_v3: false
    nfs_v4: true
    __nfs_server: "{{ groups['nfs_servers'] | first }}"
    __nfs_client: "{{ groups['nfs_clients'] | first }}"
    export_path: /export/test
    server: "{{ ( inventory_hostname | regex_replace('-client', '-server')) }}"
  tasks:

    - name: Setup NFS client
      ansible.builtin.include_role:
        name: nfs
      vars:
        nfs_server: false
        nfs_mounts:
          - { src: "{{ server }}:{{ export_path }}", target: /mnt, type: 'nfs', options: 'rw,sync' }
</pre></code>
