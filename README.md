
williamyeh.consul_exporter for Ansible Galaxy
============

[![Circle CI](https://circleci.com/gh/William-Yeh/ansible-consul-exporter.svg?style=shield)](https://circleci.com/gh/William-Yeh/ansible-consul-exporter) [![Build Status](https://travis-ci.org/William-Yeh/ansible-consul-exporter.svg?branch=master)](https://travis-ci.org/William-Yeh/ansible-consul-exporter)



## Summary

Role name in Ansible Galaxy: **[williamyeh.consul_exporter](https://galaxy.ansible.com/williamyeh/consul_exporter/)**

This Ansible role has the following features for [consul_exporter](https://github.com/prometheus/consul_exporter) (a [Consul](https://github.com/hashicorp/consul) metrics exporter for [Prometheus](http://prometheus.io/)):

 - Install specific versions of consul_exporter;
 - Install by compiling from the *master* repo;
 - Handlers for restart/reload/stop events;
 - Bare bone configuration (*real* configuration should be left to user's template files; see **Usage** section below).




## Role Variables


### Mandatory variables

None.


### Optional variables: version

Install specific version of Consul exporter (a little bit outdated; I hope the maintainer of consul_exporter will provide more recent binary releases):

```yaml
# default version
prometheus_consul_exporter_version: 0.2.0
```

Or, you can optionally download/compile from the *master* branch of consul_exporter by setting the respective version to `git`:

```yaml
prometheus_consul_exporter_version: git
```

It will install a temporary Golang compiler in the `prometheus_workdir` directory (defined in `defaults/main.yml`). If you'd like to force rebuild each time, enable the following variable (default is `false`):

```yaml
prometheus_rebuild: true
```


### Optional variables: command-line arguments


Additional command-line arguments, if any (use `consul_exporter --help` to see the full list of arguments):

```yaml
prometheus_consul_exporter_opts
```



### Optional variables: general settings of Prometheus

This section lists all variables common for all Prometheus servers and exporters. You may have seen them in my **[williamyeh.prometheus](https://galaxy.ansible.com/williamyeh/prometheus/)** role.


User-configurable defaults:

```yaml
# user and group
prometheus_user:   prometheus
prometheus_group:  prometheus


# directory for executable files
prometheus_install_path:   /opt/prometheus

# directory for logs
prometheus_log_path:       /var/log/prometheus

# directory for PID files
prometheus_pid_path:       /var/run/prometheus



# directory for temporary files
prometheus_download_path:  /tmp


# version of helper utility "gosu"
gosu_version:  1.9
```



## Handlers

- `restart consul_exporter`

- `reload consul_exporter`

- `stop consul_exporter`


## Usage


### Step 1: add role

Add role name `williamyeh.consul_exporter` to your playbook file.


### Step 2: add variables

Set vars in your playbook file, if necessary.

Simple example:

```yaml
---
# file: simple-playbook.yml

- hosts: all
  become: True
  roles:
    - williamyeh.consul_exporter

  vars:

    prometheus_consul_exporter_opts: "-log.level=debug"
```



## Dependencies

None.


## Contributors

- [William Yeh](https://github.com/William-Yeh)
- [Robbie Trencheny](https://github.com/robbiet480) - contribute an early version of building binaries from Go source code.
- [Travis Truman](https://github.com/trumant) - contribute an early version of this role.
- [Musee Ullah](https://github.com/lae) - test with [`savagegus.consul`](https://github.com/savagegus/ansible-consul) role.

## License

MIT License. See the [LICENSE file](LICENSE) for details.
