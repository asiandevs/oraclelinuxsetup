# oraclelinuxsetup
README FILE: Linux setup for Oracle Software Installation

oracle readiness for Oracle Database software install 
 
This Ansible Playbook can help you to to setup necessary configuration for installating Oracle Database software into the Linux environemnt.
Please make sure you modify the necessary variables as per your own setup. Always play/test into lower setup multiple times before implementing into the 
actual live system.

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
Summary Steps with this Ansible playbook are as below : 
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
# # Manage User Equivalency between all nodes of a cluster
# Configuring Network Time Protocol (NTPD)
# Setting shell limits
# 1. Set kernel parameters
# 2. Install required operating system packages
# 3. Disable firewalls
# 4. Create necessary OS groups and users
# 5. Create necessary OS users
# 6. Set up shell limit for oracle user
# 7. Set up shell limit for grid user
# 8. Update /etc/hosts file entry
# 9. Create required directories
# 10.configure user equivalence
# 11. Install Oracle Pre-Install RPM
# 12. Editing profile entries
# ============================================================

Tree Structure for this playbook is as below - 

[root@oel75 tasks]# tree /etc/ansible/roles/linuxfororacle_prep
/etc/ansible/roles/linuxfororacle_prep
├── tasks
│   ├── create_required_dirs.yml
│   ├── grid_bash_profile.yml
│   ├── grid_users.yml
│   ├── main.yml
│   ├── oracle_bash_profile.yml
│   ├── oracle_cp_preinstallfile.yml
│   ├── oracle_db_preinstallfile.yml
│   ├── oracle_disable_firewall.yml
│   ├── oracle_grid_shell_limit.yml
│   ├── oracle_groups.yml
│   ├── oracle_host_fileupdate.yml
│   ├── oracle_kernelparams.yml
│   ├── oracle_packages.yml
│   ├── oracle_ssh_equi.yml
│   ├── oracle_users_shell_limit.yml
│   └── oracle_users.yml
├── templates
│   └── oracle-database-preinstall-19c-1.0-1.el7.x86_64.rpm
└── vars
    └── main.yml


Note: 
i)  Modify parameters valuess based on your requirements [ /etc/ansible/roles/linuxfororacle_prep/vars/main.yml]
ii) For testing  one can disable indiviaul playbook under main.yml file [/etc/ansible/roles/linuxfororacle_prep/tasks]
iii) you can use with option --check / --diff / -v[v][v]
To execute: 

ansible-playbook linux_oracle.yml --check 
ansible-playbook linux_oracle.yml --check --diff

Sample Run:
[root@oel75 ansible]# ansible-playbook linux_oracle.yml

PLAY [opsdev] ***************************************************************************************************

TASK [Gathering Facts] ******************************************************************************************
ok: [opsdev]

TASK [linuxfororacle_prep : display pre installation of setting up Linux  software message] *********************
ok: [opsdev] => {
    "msg": [
        "This playbook is for setting Oracle  database software 19c at 2019-09-14T22:57:45Z:"
    ]
}

TASK [linuxfororacle_prep : setup necessary kernel parameters] **************************************************
ok: [opsdev] => (item={u'name': u'fs.file-max', u'value': 6815744})
ok: [opsdev] => (item={u'name': u'kernel.sem', u'value': u'250 32000 100 128'})
ok: [opsdev] => (item={u'name': u'kernel.shmmni', u'value': 4096})
ok: [opsdev] => (item={u'name': u'kernel.shmall', u'value': 1073741824})
ok: [opsdev] => (item={u'name': u'kernel.shmmax', u'value': 4398046511104})
ok: [opsdev] => (item={u'name': u'kernel.panic_on_oops', u'value': 1})
ok: [opsdev] => (item={u'name': u'net.core.rmem_default', u'value': 262144})
ok: [opsdev] => (item={u'name': u'net.core.rmem_max', u'value': 4194304})
ok: [opsdev] => (item={u'name': u'net.core.wmem_default', u'value': 262144})
ok: [opsdev] => (item={u'name': u'net.core.wmem_max', u'value': 1048576})
ok: [opsdev] => (item={u'name': u'net.ipv4.conf.all.rp_filter', u'value': 2})
ok: [opsdev] => (item={u'name': u'net.ipv4.conf.default.rp_filter', u'value': 2})
ok: [opsdev] => (item={u'name': u'fs.aio-max-nr', u'value': 1048576})
ok: [opsdev] => (item={u'name': u'net.ipv4.ip_local_port_range', u'value': u'9000 65500'})

TASK [linuxfororacle_prep : Install required libraries] *********************************************************
ok: [opsdev]

TASK [linuxfororacle_prep : Stop and disable FIREWALLD] *********************************************************
ok: [opsdev]

TASK [linuxfororacle_prep : Create user] ************************************************************************
changed: [opsdev] => (item=dba)
changed: [opsdev] => (item=oinstall)
changed: [opsdev] => (item=oper)
changed: [opsdev] => (item=asmdba)
changed: [opsdev] => (item=asmdba)

TASK [linuxfororacle_prep : Create user] ************************************************************************
changed: [opsdev] => (item=dba)
changed: [opsdev] => (item=oinstall)
changed: [opsdev] => (item=oper)
changed: [opsdev] => (item=asmdba)
changed: [opsdev] => (item=asmdba)

TASK [linuxfororacle_prep : Add oracle user limits] *************************************************************
changed: [opsdev] => (item={u'limit': u'soft', u'type': u'nofile', u'value': 4096})
changed: [opsdev] => (item={u'limit': u'hard', u'type': u'nofile', u'value': 65536})
changed: [opsdev] => (item={u'limit': u'soft', u'type': u'nproc', u'value': 2047})
changed: [opsdev] => (item={u'limit': u'hard', u'type': u'nproc', u'value': 16384})
changed: [opsdev] => (item={u'limit': u'soft', u'type': u'stack', u'value': 10240})
changed: [opsdev] => (item={u'limit': u'hard', u'type': u'stack', u'value': 32768})
changed: [opsdev] => (item={u'limit': u'soft', u'type': u'memlock', u'value': 1887437})
changed: [opsdev] => (item={u'limit': u'hard', u'type': u'memlock', u'value': 1887437})

TASK [linuxfororacle_prep : Add grid user limits] ***************************************************************
changed: [opsdev] => (item={u'limit': u'soft', u'type': u'nofile', u'value': 4096})
changed: [opsdev] => (item={u'limit': u'hard', u'type': u'nofile', u'value': 65536})
changed: [opsdev] => (item={u'limit': u'soft', u'type': u'nproc', u'value': 2047})
changed: [opsdev] => (item={u'limit': u'hard', u'type': u'nproc', u'value': 16384})
changed: [opsdev] => (item={u'limit': u'soft', u'type': u'stack', u'value': 10240})
changed: [opsdev] => (item={u'limit': u'hard', u'type': u'stack', u'value': 32768})
changed: [opsdev] => (item={u'limit': u'soft', u'type': u'memlock', u'value': 1887437})
changed: [opsdev] => (item={u'limit': u'hard', u'type': u'memlock', u'value': 1887437})

TASK [linuxfororacle_prep : Update the /etc/hosts file with node name] ******************************************
changed: [opsdev] => (item=opsdev)

TASK [linuxfororacle_prep : create required directories] ********************************************************
changed: [opsdev] => (item=/u02)
changed: [opsdev] => (item=/u02/stage)
changed: [opsdev] => (item=/u02/app)

TASK [linuxfororacle_prep : SSH KeyGen command] *****************************************************************
ok: [opsdev]

TASK [linuxfororacle_prep : Fetch the keyfile from one server to another] ***************************************
ok: [opsdev]

TASK [linuxfororacle_prep : Copy the key add to authorized_keys using Ansible module] ***************************

TASK [linuxfororacle_prep : copy database pre install file to the target database server] ***********************
changed: [opsdev] => (item=oracle-database-preinstall-19c-1.0-1.el7.x86_64.rpm)

TASK [linuxfororacle_prep : install predbinstall rpm from a local file] *****************************************
changed: [opsdev]

TASK [linuxfororacle_prep : bash_profile for oracle user] *******************************************************
changed: [opsdev]

TASK [linuxfororacle_prep : bash_profile for oracle grid] *******************************************************
changed: [opsdev]

PLAY RECAP ******************************************************************************************************
opsdev                     : ok=17   changed=10   unreachable=0    failed=0
