Ansible Role: JRE
=========
[![Build Status](https://travis-ci.org/cmprescott/ansible-role-jre.svg?branch=master)](https://travis-ci.org/cmprescott/ansible-role-jre)

Installs the Java Runtime Engine (JRE). Defaults to Oracle Server JRE on Linux. Optional: Install OpenJDK JRE using apt, yum, or pkgng.

Requirements
------------

```shell
# Ansible version 2.1+
ansible --version

# ----- For Oracle Server JRE -----
# Ansible's uri module requires Python httplib2
pip install httplib2

# Oracle server JRE requires 64 bit remote CPU 
lscpu | grep Architecture

# ----- For OpenJDK JRE -----
case $OSTYPE in
  # Linux needs apt|yum
  "linux"*)
      apt --version||yum --version;;
  # FreeBSD needs pkgng (Versions 9+)
  "freebsd"*)
      pkg -version;;
esac
```

Role Variables
--------------

```yaml
# Prefer Oracle Server JRE when possible?
jre_prefer_oracle: true

# OpenJDK version settings
jre_open_jdk_version: "8"

# Oracle version, download, installation settings
jre_oracle_version: 8u73
jre_oracle_download_url: "http://download.oracle.com/otn-pub/java/jdk/{{ jre_oracle_version }}-b02/server-jre-{{ jre_oracle_version }}-linux-x64.tar.gz"
jre_oracle_download_referrer: "http://www.oracle.com/technetwork/java/javase/downloads/server-jre8-downloads-2133154.html"
jre_oracle_download_cookie: >
  atgPlatoStop=1;
  oraclelicense=accept-securebackup-cookie
  s_cc=true;
  ARU_LANG=US;
  s_nr=1458606516696;
  gpw_e24={{ jre_oracle_download_referrer }}
  s_sq="%"5B"%"5BB"%"5D"%"5D"
jre_oracle_download_dest: /tmp/jre.tar.gz
jre_oracle_install_dir: /usr/lib/jvm/jre_1.{{ jre_oracle_version }}
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
