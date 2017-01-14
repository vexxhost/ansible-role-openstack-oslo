Oslo
====
This role helps configure any applications which use `oslo`.  It also has
helpers to configure the specific components such as databases.


Requirements
------------
This role is typically used within other rules with an `include_role`.  It
is not designed to run standalone.


Role Variables
--------------
The variables that have to be configured inside this role are the following:

| Variable                         | Description                            |
| -------------------------------- | -------------------------------------- |
| `openstack_oslo_db_manage`       | Enable managing creation of databases  |
| `openstack_oslo_db_driver`       | Control the database driver for `oslo` |
| `openstack_oslo_db_name`         | Database name                          |
| `openstack_oslo_db_username`     | Database username                      |
| `openstack_oslo_db_password`     | Database password                      |
| `openstack_oslo_db_config_files` | List of configuration files to update  |


Dependencies
------------
This role has no dependencies besides built-in stable Ansible modules


Example Usage
-------------

    - name: configure database
      include_role:
        name: vexxhost.openstack-oslo
        tasks_from: db
      vars:
        openstack_oslo_db_manage: "{{ openstack_keystone_manage_database | default(omit) }}"
        openstack_oslo_db_driver: "{{ openstack_keystone_database_driver | default(omit) }}"
        openstack_oslo_db_name: "{{ openstack_keystone_database_name }}"
        openstack_oslo_db_username: "{{ openstack_keystone_database_username }}"
        openstack_oslo_db_password: "{{ openstack_keystone_database_password }}"
        openstack_oslo_db_config_files:
          - "{{ __openstack_keystone_config_file }}"
      notify:
        - sync keystone database
        - bootstrap keystone database


License
-------
Apache


Author Information
------------------
http://vexxhost.com
