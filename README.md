ansible-dts
=========

Deploys [dts4](http://www.apelondts.org/).

Requirements
------------

This role requires a working java JRE 7, JBoss 7.1, and mysql 5.6 install.  If you need these as well, here are roles that work well with this role.

* https://github.com/yatesr/ansible-java
* https://github.com/yatesr/ansible-jboss
* https://github.com/yatesr/ansible-mysql


Role Variables
--------------

```

# Location dts will be installed to
dts_install_dir: /opt/dts

# dts mysql user password. If you are using the mysql module see this equal to the dts4user password.
dts_mysql_password: dts4password
dts_mysql_root_password: root

# Deploy dts from local archive? (You probably don't want this)
dts_deploy: false
# dts archive location
dts_archive_loc:

# Name of jboss service
dts_jboss_service: "jboss"
# JBoss home folder.  If using with jboss a role reference this in your play.
dts_jboss_home_dir: /opt/jboss/jboss-as-7.1.1.Final
# JBoss dtsuser password
dts_user_password: dts
dts_admin_password: dtsadmin
apelon_admin_password: apelonadmin


# Version of DTS 4 to download
dts_version_full: "4.1.0.377"
dts_version_short: "4.1"
dts_download_url: "http://www.apelondts.org/Portals/0/Downloads/DTS%20{{dts_version_short}}/dts-linux_{{dts_version_full}}.tar.gz"


```

Example Playbook
----------------

```

---
- hosts: all
  roles:
   - ansible-java
   - ansible-mysql
   - ansible-jboss
   - ansible-dts
  vars:
     dts_jboss_home_dir: /opt/jboss/jboss-as-7.1.1.Final
     jboss_base_dir: /opt/jboss
     dts_mysql_password: "dts4password"
     dts_mysql_root_password: "root"
     # MySQL role vars below
     mysql_root_password: root
     mysql_server_version: -5.6
     mysql_users:
       dts4user:
         password: dts4password
         priv: "dts4.*:ALL"
     mysql_dbs:
       dts4:


```


License
-------

Apache v2

Author Information
------------------

Ryan Yates
