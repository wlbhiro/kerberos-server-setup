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


REQUIRED OPERATION COMMANDS
------------------------------

```
export KRB5_SERVER="kerberos-server.local"
sudo bash -c "echo '${KRB5_SERVER}' > /etc/hostname"
sudo bash -c "hostname ${KRB5_SERVER}"
### HAVE TO RELOGIN ###
```


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


Kerberos(KDC) Operation Check Command
----------------------------------------

```
[root@kerberos-server ~]# kadmin.local
Authenticating as principal root/admin@LOCAL with password.
kadmin.local:  add_principal root
WARNING: no policy specified for root@LOCAL; defaulting to no policy
Enter password for principal "root@LOCAL": 
Re-enter password for principal "root@LOCAL": 
Principal "root@LOCAL" created.
kadmin.local:  exit
[root@kerberos-server ~]# kinit root
Password for root@LOCAL: 
[root@kerberos-server ~]# klist -e
Ticket cache: KEYRING:persistent:0:0
Default principal: root@LOCAL

Valid starting       Expires              Service principal
11/16/2018 11:39:35  11/17/2018 11:39:35  krbtgt/LOCAL@LOCAL
Etype (skey, tkt): aes256-cts-hmac-sha1-96, aes256-cts-hmac-sha1-96 
[root@kerberos-server ~]# 
```


Trouble Shooting (Error krb5-libs Install)
--------------------------------------------

Error : 

```
--> Finished Dependency Resolution
Error: Package: krb5-server-1.15.1-18.el7.x86_64
        Requires: krb5-libs(x86-64) = 1.15.1-18.el7
        Installed: krb5-libs-1.15.1-19.el7
        ...........
```

Solve : 

```
sudo yum downgrade krb5-libs
```

License
-------

MIT

Author Information
------------------

Hirofumi Kawasaki

