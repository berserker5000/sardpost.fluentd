Role Name: sardpost.fluentd
=========

Ansible role for installing fluentd(td-agent) on EL 7 platform (RHEL/Centos 7).
A series of tasks are executed before installing fluentd, some are highly
recommended to configure the environment to prevent unnecessary problems.
WARNING: After the first tasks are completed succesfully the server gets rebooted.  
Pre tasks can be disabled setting to "False" the variable "pre_install" in
defaults/main.yml.
The role installs td-agent from the official repository.
Features:

```yml
          Pre tasks:
          - Increase Max number of File Descriptors in /etc/security/limits.conf
          - Optimize Network Kernel Parameters in /etc/sysctl.conf
          Tasks:
          - Import GPG key for official repository
          - Install rpm Repository
          - Install td-agent
          - Install fluent-plugin-elasticsearch
          - Launch td-agent daemon
          - Set Up rsyslogd to forward the logs to fluentd(td-agent)
          - Restart rsyslogd service
```
Refer to the official documentation page for further information:

```yml
          http://docs.fluentd.org/articles/before-install
```

Requirements
------------

```yml
        - RHEL/Centos 7
        - ntpd to prevent invalid timestamps in your logs
```

Role Variables
--------------
If a custom configuration file needs to be specified copying the customed configuration
file in files/td-agent.conf and setting to "True" the variable "custom_conf_file" in
defaults/main.yml

```yml
        custom_conf_file: True
```

Dependencies
------------

```yml
      - yaegashi.blockinfile  #not needed in Ansible 2 as part of core modules
```


Example Playbook
----------------

```yml
  - name: Install fluentd(td-agent)
    hosts: test_lab
    remote_user: centos
    sudo: yes

    roles:
      - sardpost.fluentd
      - yaegashi.blockinfile
```

Version:
--------
0.1

License
-------
GPLv3

Author Information
------------------
Davide M. Puggioni
