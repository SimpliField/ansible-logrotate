Logrotate
=========

Setup logrotate

Requirements
------------

Need ansible 2

Role Variables
--------------

```yaml
logrotate_include_dir: /etc/logrotate.d
logrotate_options:
- weekly
- su root syslog
- rotate 4
- create

logrotate_wtmp:
  logs:
  - /var/log/wtmp
  options:
  - missingok
  - monthly
  - create 0664 root utmp
  - rotate 1

logrotate_btmp:
  logs:
  - /var/log/btmp
  options:
  - missingok
  - monthly
  - create 0660 root utmp
  - rotate 1

logrotate_applications: []
```

Dependencies
------------

There is no dependencies

Example Playbook
----------------

```yaml
- hosts: servers
  roles:
  - role: SimpliField.logrotate
    logrotate_applications:
    - name: apt
      definitions:
      - logs:
        - /var/log/apt/term.log
        - /var/log/apt/history.log
        options:
          - rotate 12
          - monthly
          - missingok
          - notifempty
          - compress
```

License
-------

BSD
