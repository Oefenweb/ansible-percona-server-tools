## percona-server-tools

[![Build Status](https://travis-ci.org/Oefenweb/ansible-percona-server-tools.svg?branch=master)](https://travis-ci.org/Oefenweb/ansible-percona-server-tools) [![Ansible Galaxy](http://img.shields.io/badge/ansible--galaxy-percona--server--tools-blue.svg)](https://galaxy.ansible.com/list#/roles/5042)

Manage [percona-server](https://www.percona.com/software/mysql-database/percona-server) server (or any other flavour of MySQL) in Debian-like systems.

#### Requirements

* `mysql` (will not be installed)
* `mysqld` (will not be installed)

#### Variables

##### Reset root password

* `percona_server_tools_reset_root_password`: [default: `false`]: Whether or not to run `reset-root-password.yml`
* `percona_server_tools_reset_root_password_root_password`: [required]: Root password

##### Resize InnoDB logs

* `percona_server_tools_reset_ib_logfile`: [default: `false`]: Whether or not to run `reset-ib-logfile.yml`
* `percona_server_tools_reset_ib_logfile_ib_logfiles`: [default: `[/var/lib/mysql/ib_logfile0, /var/lib/mysql/ib_logfile1]`]: InnoDB logs to resize

## Dependencies

None

## Recommended

* `percona-client` ([see](https://github.com/Oefenweb/ansible-percona-client)
* `percona-server` ([see](https://github.com/Oefenweb/ansible-percona-server)

#### Example(s)

##### Reset root password

```yaml
---
- hosts: all
  roles:
    - percona-server-tools
  vars:
    percona_server_tools_reset_root_password: true
    percona_server_tools_reset_root_password_root_password: '6j~14F(Um~@nAz4hn6dT'
```

##### Resize InnoDB logs

```yaml
---
- hosts: all
  roles:
    - percona-server-tools
  vars:
    percona_server_tools_reset_ib_logfile: true
```

#### License

MIT

#### Author Information

Mischa ter Smitten

#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/Oefenweb/ansible-percona-server-tools/issues)!
