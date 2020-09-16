# Ansible Filebeat
[![Build Status](https://travis-ci.com/supertarto/ansible-filebeat.svg?branch=master)](https://travis-ci.com/supertarto/ansible-filebeat)

Install and configure filebeat.
This role is meant for my small need, so the only output configured in template is logstash for now.

Tested with v7.9.0

## Tested plateform
* Debian 10 (Buster)

## Role variables
Filebeat version, and informations used during the installation.
```yml
filebeat_version: "7.9.0"
filebeat_repo_base: "https://artifacts.elastic.co"
filebeat_apt_key: "{{ filebeat_repo_base }}/GPG-KEY-elasticsearch"
filebeat_apt_key_id: "46095ACC8548582C1A2699A9D27D666CD88E42B4"
filebeat_apt_url: "deb {{ filebeat_repo_base }}/packages/{{ filebeat_major_version }}/apt stable main"
filebeat_package_name: "filebeat"
filebeat_conf_dir: "/etc/filebeat"
```

Set to True if you want to set the package on hold, to prevent unwanted upgrade.
```yml
filebeat_version_lock: false
```

Input configurations
```yml
filebeat_inputs:
  type: log
  enabled: false
  fields:
    format: csv
    source: filebeat
  paths:
    - "/path/to/your/file"
```

Define if we use logstash as an output or not
```yml
filebeat_logstash_output: false
```

Output configurations. Tested only for logstash.
```yml
filebeat_output_hosts: somehost
filebeat_output_ssl_ca: "/path/to/ca"
filebeat_output_ssl_cert: "/path/to/cert"
filebeat_output_ssl_key: "/path/to/key"
```
## Examples
```yml
- name: Converge
  hosts: all
  roles:
    - role: supertarto.filebeat
```
## Installation
```
ansible-galaxy install supertarto.filebeat
```
## License
GPL V3.0
