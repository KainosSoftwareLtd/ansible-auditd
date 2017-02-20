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

All configuration parameters and base rules are stored in defaults:

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

You can also set your own custom rules there:

```
auditd_custom_rules: []
```

License
-------

MIT

Author Information
------------------

This role was created in 2017 by Caoimhin Graham on behalf of [Kainos Software](https://www.kainos.com).
