insights-client
========

Installs, configures, and registers a system to the Red Hat Insights using Satellite.  This role is intended to work on Red Hat Enterprise Linux, though it will generally work on any yum based system that has access to the insights-client RPM. This role may be used to register a host server to a capsule server


Role Variables
--------------

  bootstrap_target_path: /var/tmp/                       # set insighst_only to true to fix insights repo issues, runs insights-client or both
  insights_only: false                                   # used if host is already registerdd to satellite
  satellite_server_hostname: sd-425s-whcy.nam.nsroot.net # Used to prevent satellite self registration
  old_satellite_server_fqdn: sd-425s-whcy.nam.nsroot.net # needed to remove a stale satellite cert
  change_satellite: false                                # needed to remove an old cert from a system that was registered to satellite
  register_new_host: true                                # used to register new host
  satellite_org: citi                                    # used to add host to organization
  satellite_location: dallas                             # used to add host to location
  activation_key: insights                               # used to allow host access to certain repositories
  force: false                                           # used to add force flag to the bootstrap.py file
  skip:                                                  # list of software and configurations to skip
  - foreman
  - puppet
  - katello-agent
  - katello-host-tools


Example Playbook
----------------

	- hosts:        all
	  strategy:     free
	  gather_facts: false
          become:       true
          tasks:
          - include_role:
               name: insights


Note: Any of the role variables mentioned earlier can be placed in this configuration file

Change the permissions on the file so that only you can read them, and then any time you invoke
this role, add the ansible-playbook --extra-vars option:

    $ ansible-playbook ... --extra-vars @insights-role-vars.yml ...

Note that one of the really useful features of Ansible Tower is role based management of credentials
like this.



License and Author
------------------

License: Apache License 2.0
Author: Red Hat, Inc.
