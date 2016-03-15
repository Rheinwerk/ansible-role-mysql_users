MySQL Users
=========

This roles manages users and databases for a MySQL compatible DB server like MySQL, Galera etc.

[![Build Status](https://travis-ci.org/Rheinwerk/ansible-role-mysql_users.svg?branch=master)](https://travis-ci.org/Rheinwerk/ansible-role-mysql_users)

Requirements
------------

None.

Role Variables
--------------

There are two variables that drive this role: `_mysql_users` and `RW_APT_CACHE_UPDATE`. `_mysql_users` is a map that contains all configuration and settings for this role. `RW_APT_CACHE_UPDATE` may be specified as an _extra variable_ on invocation of Ansible in order to force `apt-get update`.

Dependencies
------------

None.

Example Playbook
----------------

The general contract of this role is to take the variables map `_mysql_users` from `defaults/main.yml` as a template for your configuration and pass that configuration as a parameter to this role.

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:
```
    - hosts: <HOST THAT IS ALLOWED TO MANAGE MYSQL>
      var:
        MYSQL_USERS:
          host: <HOST MYSQL IS RUNNING ON>
          root:
            password: <ADMIN_PASSWORD>
          users:
            grafana:
              state: present
              name: grafana
              password: <DB_USER_PASSWORD>
              privileges: "grafana.*:ALL,GRANT"
              hosts:
                - <HOST ALLOWED TO QUERY>
          databases:
            grafana:
              name: grafana
              state: present
      roles:
         - { role: mysql_users, tags: [ 'mysql_users' ], _mysql_users: "{{ MYSQL_USERS }}" }
```

License
-------

Please see LICENSE.

Author Information
------------------

Original author is [Lukas Pustina](https://github.com/lukaspustina) as member of the [Rheinwerk](https://github.com/Rheinwerk) project.
