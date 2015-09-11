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

##### Setup slave replication (using `xtrabackup`)

* `percona_server_tools_setup_slave_replication`: [default: `false`]: Whether or not to run `setup-slave-replication.yml`
* `percona_server_tools_setup_slave_replication_master`: [required]: The inventory hostname of the master server (e.g. `db-01.example.com`)
* `percona_server_tools_setup_slave_replication_slaves`: [required]: The inventory hostname(s) of the slave server(s) (e.g. `[db-02.example.com, db-03.example.com]`)

* `percona_server_tools_setup_slave_replication_innobackupex_user`: [optional]: Specifies the user (i.e., the MySQL username used when connecting to the server) to login as, if that’s not the current user. It is passed to the `mysql` child process without alteration
* `percona_server_tools_setup_slave_replication_innobackupex_password`: [optional]: Specifies the password to use when connecting to the database. It is passed to the `mysql` child process without alteration
* `percona_server_tools_setup_slave_replication_innobackupex_parallel`: [optional]: Specifies the number of threads the `xtrabackup` child process should use to back up files concurrently
* `percona_server_tools_setup_slave_replication_innobackupex_rsync`: [optional]: Use the `rsync` utility to optimize local file transfers. When this option is specified, `innobackupex` uses `rsync` to copy all non-InnoDB files instead of spawning a separate `cp` for each file, which can be much faster for servers with a large number of databases or tables
* `percona_server_tools_setup_slave_replication_innobackupex_backup_dir`: [required]: Specifies the backup directory
* `percona_server_tools_setup_slave_replication_innobackupex_use_memory`: [optional]: Specifies the amount of memory in bytes for `xtrabackup` to use for crash recovery while preparing a backup

* `percona_server_tools_setup_slave_replication_master_host`: [required]: Specifies the `MASTER_HOST`, needed to setup the replication, but also the pull backups from the master (`rsync` over `ssh`) (e.g. `{{ hostvars[percona_server_tools_setup_slave_replication_master]['ansible_eth1']['ipv4']['address'] }}`)
* `percona_server_tools_setup_slave_replication_master_user`: [required]: Specifies the `MASTER_USER` (e.g. `replicator`)
* `percona_server_tools_setup_slave_replication_master_password`: [required]: Specifies the `MASTER_PASSWORD`

## Dependencies

None

## Recommended

* `percona-client` ([see](https://github.com/Oefenweb/ansible-percona-client))
* `percona-server` ([see](https://github.com/Oefenweb/ansible-percona-server))
* `ssh-keys` ([see](https://github.com/Oefenweb/ansible-ssh-keys))

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

##### Setup slave replication

```yaml
---
- hosts: all
  roles:
    - percona-server-tools
  vars:
    percona_server_tools_setup_slave_replication: true
    percona_server_tools_setup_slave_replication_master: db-01.example.com
    percona_server_tools_setup_slave_replication_slaves:
      - db-02.example.com
    
    percona_server_tools_setup_slave_replication_innobackupex_backup_dir: /tmp/xtrabackup
    
    percona_server_tools_setup_slave_replication_master_host: "{{ hostvars[percona_server_tools_setup_slave_replication_master]['ansible_eth1']['ipv4']['address'] }}"
    percona_server_tools_setup_slave_replication_master_user: replicator
    percona_server_tools_setup_slave_replication_master_password: 'Z$8>YM"KUVRv6sW#=O-A'
```

#### License

MIT

#### Author Information

Mischa ter Smitten

#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/Oefenweb/ansible-percona-server-tools/issues)!
