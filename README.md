Role Name
=========

Role Name : kerberos-server-setup



Operational confirmation environment
-------------------------------------

uname -a : Linux kerberos-server.local 3.10.0-862.el7.x86_64 #1 SMP Fri Apr 20 16:44:24 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux

```
[wlbhiro@kerberos-server ~]$ rpm -qa | fgrep krb
krb5-server-1.15.1-19.el7.x86_64
krb5-devel-1.15.1-19.el7.x86_64
krb5-workstation-1.15.1-19.el7.x86_64
krb5-libs-1.15.1-19.el7.x86_64
```

```
[wlbhiro@kerberos-server ~]$ rpm -qa | fgrep ansible
ansible-2.4.2.0-2.el7.noarch
```

Requirements
------------

OS : CentOS 7 (Redhat)

Ansible Version : 2.4

Kerberos Version : 5(1.15)


Role Variables
--------------

```
kerberos:
  kdc: kerberos-server.local
  admin_server: kerberos-server.local
  realm: local
  kdc_ports: 88
  kdc_tcp_ports: 88
  master_pass: password
  kadmin_user: kadmin_user
  kadmin_pass: password
```

Dependencies
------------

No.

Example Playbook
----------------

    - hosts: kerberos-server
      roles:
         - { role: wlbhiro.kerberos-server-setup, 
                 kerberos.kdc: kerberos-server.local,
                 kerberos.admin_server: kerberos-server.local,
                 kerberos.realm: local,
                 kerberos.kdc_ports: 88,
                 kerberos.kdc_tcp_ports: 88,
                 kerberos.master_pass: password,
                 kerberos.kadmin_user: kadmin_user,
                 kerberos.kadmin_pass: password
            }

License
-------

MIT

Author Information
------------------

Hirofumi Kawasaki

