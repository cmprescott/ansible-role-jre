Ansible Role: JRE
=========
[![Build Status](https://travis-ci.org/cmprescott/ansible-role-jre.svg?branch=master)](https://travis-ci.org/cmprescott/ansible-role-jre)

Downloads & installs the Oracle JRE. Defaults to Oracle Server JRE.

Requirements
------------

```shell
# Ansible's uri module requires Python httplib2
pip install httplib2

# Ansible version > 1.6
ansible --version

# Oracle server JRE requires 64 bit remote CPU 
lscpu | grep Architecture
```

Role Variables
--------------

```yaml
# Prefer Oracle Server JRE when possible?
jre_prefer_oracle: true

# Download settings
jre_oracle_version: 8u73
jre_oracle_download_url: "http://download.oracle.com/otn-pub/java/jdk/{{ jre_version }}-b14/server-jre-{{ jre_version }}-linux-x64.tar.gz"
jre_oracle_download_referrer: "http://www.oracle.com/technetwork/java/javase/downloads/server-jre8-downloads-2133154.html" 
jre_oracle_download_cookie: >
  atgPlatoStop=1; 
  oraclelicense=accept-securebackup-cookie; 
  s_cc=true; 
  ARU_LANG=US; 
  s_nr=1430222185739; 
  gpw_e24={{ jre_download_referrer }}
  s_sq="%"5B"%"5BB"%"5D"%"5D"
jre_oracle_download_dest: /tmp/jre.tar.gz
jre_oracle_install_dir: /usr/lib/jvm/jre_1.{{ jre_version }}
jre_oracle_install_bins: [ 'java', 'javac' ]
```

Dependencies
------------

None.

Example Playbook
----------------

```yaml
- hosts: servers
  roles:
     - role: cmprescott.jre
```

License
-------

BSD

Author Information
------------------

Prescott Chris
