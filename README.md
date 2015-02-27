uchiwa
======

Role to install Uchiwa dashboard for Sensu.

The configuraton of the role is done in such way that it should not be necessary
to change the role for any kind of configuration. All can be done either by
changing role parameters or by declaring completely new configuration as a
variable. That makes this role absolutely universal. See the examples below for
more details.

Please report any issues or send PR.


Examples
--------

```
# Example of usage with default configuration
- hosts: myhost1
  roles:
    - uchiwa

# Example of how to adapt the default configuration
- hosts: myhost2
  vars:
    uchiwa_sensu_site: "DataCentre 1"
    uchiwa_sensu_ssl_enabled: "true"
    uchiwa_sensu_timeout: 5
    uchiwa_user: "uchiwa"
    uchiwa_password: "password"
  roles:
    - uchiwa

# Example of how to add more Sensu servers
- hosts: myhost3
  vars:
    uchiwa_sensu:
      - name: Sensu1
        ...
      - name: Sensu2
        ...
  roles:
    - uchiwa
```

See [Uchiwa documentation](https://uchiwa.io/#/docs/config) for more information
about the configuration.

This role requires [Jinja2 Encoder
Macros](https://github.com/picotrading/jinja2-encoder-macros) which must be
placed into the same directory as the playbook:

```
$ ls -1 *.yaml
site.yaml
$ git clone https://github.com/picotrading/jinja2-encoder-macros.git ./templates/encoder
```


Role variables
--------------

List of variables used by the role:

```
# YUM repo URL
uchiwa_yum_repo_url: http://repos.sensuapp.org/yum/el/$releasever/$basearch/

# Package to be installed (you can force a specific version here)
uchiwa_pkg: uchiwa

# Default Sensu config variables
uchiwa_sensu_site: Sensu
uchiwa_sensu_host: 127.0.0.1
uchiwa_sensu_ssl_enabled: "false"
uchiwa_sensu_port: 4567
uchiwa_sensu_user: ""
uchiwa_sensu_pass: ""
uchiwa_sensu_path: ""
uchiwa_sensu_timeout: 5000

# Default Sensu config
uchiwa_sensu:
  - name: "{{ uchiwa_sensu_site }}"
    host: "{{ uchiwa_sensu_host }}"
    ssl: "{{ uchiwa_sensu_ssl_enabled }}"
    port: "{{ uchiwa_sensu_port }}"
    user: "{{ uchiwa_sensu_user }}"
    pass: "{{ uchiwa_sensu_pass }}"
    path: "{{ uchiwa_sensu_path }}"
    timeout: "{{ uchiwa_sensu_timeout }}"

# Default Uchiwa config variables
uchiwa_host: 0.0.0.0
uchiwa_port: 3000
uchiwa_user: admin
uchiwa_pass: admin
uchiwa_refresh: 10000

# Default Uchiwa config
uchiwa_config:
  sensu: "{{ uchiwa_sensu }}"
  uchiwa:
    host: "{{ uchiwa_host }}"
    user: "{{ uchiwa_user }}"
    pass: "{{ uchiwa_pass }}"
    port: "{{ uchiwa_port }}"
    refresh: "{{ uchiwa_refresh }}"
```


Dependencies
------------

* [`yumrepo`](https://github.com/picotrading/ansible-yumrepo) role
* [Jinja2 Encoder Macros](https://github.com/picotrading/jinja2-encoder-macros)


License
-------

MIT


Author
------

Robert Readman, Jiri Tyr
