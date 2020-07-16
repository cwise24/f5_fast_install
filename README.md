Role: f5_fast_install
=========

F5 Application Services Templates (FAST) are an easy and effective way to deploy applications on the BIG-IP system using AS3.

The FAST Extension provides a toolset for templating and managing AS3 Applications on BIG-IP. This role will check tmos not below 13.1 (required) and that AS3 3.16 or greater is installed prior to downloading the checksum and RPM for installation. To validate installation the iControl endpoint `https://<mgmt ip>/mgmt/shared/iapp/installed-packages` is checked.

Requirements
------------

F5 Application Service Templates (FAST) relies on AS3 >=3.16 being installed. This role will check for tmos version and AS3 versioning. Please use f5_as3_install role prior.

*TMOS v13*
If tmos version 13 is detected the bash script `touch /var/config/rest/iapps/enable` is invoked. 

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

```
fastTag: "v1.1.0"
fastRPM: "f5-appsvcs-templates-1.1.0-1.noarch.rpm"
fastSha: "{{ fastRPM +'.sha256'}}"
f5_mgmt: "{{ hostvars[groups['adc'][0]]['ansible_host'] }}"
e_user: "admin"
e_pass: "secret"
roles_d: "."
provider:
  user: "{{ e_user }}"
  password: "{{ e_pass }}"
  server: "{{ f5_mgmt }}"
  validate_certs: no
```

Dependencies
------------

F5 Application Service Templates relies on AS3 >=3.16 being installed. This role will check for tmos version and AS3 versioning. Please use f5_as3_install role prior.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: [adc]
      gather_facts: false
      connection: local
      
      roles:
         - f5_fast_install

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
