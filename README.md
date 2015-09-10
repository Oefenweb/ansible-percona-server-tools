## percona-server-tools

[![Build Status](https://travis-ci.org/Oefenweb/ansible-percona-server-tools.svg?branch=master)](https://travis-ci.org/Oefenweb/ansible-percona-server-tools) [![Ansible Galaxy](http://img.shields.io/badge/ansible--galaxy-percona--server--tools-blue.svg)](https://galaxy.ansible.com/list#/roles/5042)

Manage [percona-server](https://www.percona.com/software/mysql-database/percona-server) server (or any other flavour of MySQL) in Debian-like systems.

#### Requirements

* `mysql` (will not be installed)
* `mysqld` (will not be installed)

#### Variables

None

## Dependencies

None

## Recommended

* `percona-client` ([see](https://github.com/Oefenweb/ansible-percona-client)
* `percona-server` ([see](https://github.com/Oefenweb/ansible-percona-server)

#### Example(s)

```yaml
---
- hosts: all
  roles:
    - percona-server-tools
```

#### License

MIT

#### Author Information

Mischa ter Smitten

#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/Oefenweb/ansible-percona-server-tools/issues)!
