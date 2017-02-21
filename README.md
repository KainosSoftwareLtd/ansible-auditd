Auditd
=========

A role that installs and configures auditd.

The role is configurable so you can setup your own custom rules but is configured by default with the basics.

Requirements
------------

* Ansible >= 2.1
* At the moment this has only been tested with CentOS 7 servers.

Configuration
------------

All configuration parameters and base rules are stored in defaults and are configured with sensible out-of-the-box values that broadly correalate with CIS guidence:

When applying rules in your environment its intended you have a two pronged approach:

1. You have some rules you always want to deploy to every server
2. You may have some custom rules to add based on the environment/role

So in addition to the standard configuration parameters you also get `auditd_base_rules` and `auditd_custom_rules` which are both arrays.

So you would setup your default auditd config as below:

```
auditd_home: /etc/audit
auditd_disp_home: /etc/audisp
auditd_disp_syslog_active: 'no'
auditd_log_file: /var/log/audit/audit.log
auditd_log_format: raw
...

auditd_base_rules:
  - '-a always,exit -F arch=b32 -S adjtimex -S settimeofday -S stime -k time-change'
  - '-a always,exit -F arch=b64 -S adjtimex -S settimeofday -S stime -k time-change'
  - '-a always,exit -F arch=b32 -S chmod -F auid>=1000 -F auid!=4294967295 -k perm_mod'
  - '-a always,exit -F arch=b64 -S chmod -F auid>=1000 -F auid!=4294967295 -k perm_mod'
...
```

And perhaps add any custom rules you require as part of role dependencies; blank is also fine.

```
auditd_custom_rules: []
```

Beware of the `auditd_enable_immutable` variable, it makes the configration immutable between restarts. So if you set this variable to _True_ it will prevent ansible from restarting/reloading the auditd service; for this reason it is set to false by default.

License
-------

MIT

Author Information
------------------

This role was created in 2017 by Caoimhin Graham and Radosław Dobrzeniecki on behalf of [Kainos Software](https://www.kainos.com).
