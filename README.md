Uchiwa Dashboard
=======

Role to install Uchiwa dashboard for Sensu.

Example
-------
See https://uchiwa.io/#/docs/config for detailed configuration information.

```
- hosts: myhost
  roles:
    - role: uchiwa
  vars:
    sensu_site: "DataCentre 1"
    ssl_enabled: "True"
    sensu_timeout: 5
    uchiwa_user: "uchiwa"
    uchiwa_password: "password"
```

Role variables
--------------

List of variables used by the role:

```
# Sensu paths
sensu_config_dir: /etc/sensu

# Uchiwa default config for Sensu
sensu_site: "Sensu"
sensu_host: "127.0.0.1"
ssl_enabled: "false"
sensu_port: 4567
sensu_user: ""
sensu_pass: ""
sensu_path: ""
sensu_timeout: 5000

# Uchiwa default config
uchiwa_host: 0.0.0.0
uchiwa_port: 3000
uchiwa_user: "admin"
uchiwa_pass: "admin"
uchiwa_stats: 10
uchiwa_refresh: 10000
```

License
-------

MIT


Author
------

Robert Readman
