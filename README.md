galera
======

This role configures Galera/MariaDB 5.5 cluster.

Requirements
------------

You must add jinja2.ext.loopcontrols to your jinja2_extensions in your ansible.cfg. All other requirements are listed
in metadata file.

Role Variables
--------------

The variables that can be passed to this role and a brief description about
them are as follows.

	# MariaDB root user password
	galera_root_password: 1qa2ws3ed

	# MariaDB debian-sys-maint user password
	galera_maintenance_password: 1qa2ws3ed

	# Galera cluster authorization credentials
	galera_cluster_user: replicator
	galera_cluster_password: 1qa2ws3ed

	# Address MariaDB will listen on
	galera_bind_address: 127.0.0.1

	# Nodes with this parameter set to zero will be configured as standalone, i.e. wsrep_cluster_address=gcomm://
	galera_bootstrap: 0

	# Unique Galera cluster identifier
	galera_cluster_name: mycluster

	# Addresses of cluster nodes to connect to
	galera_cluster_members: [10.0.0.1, 10.0.0.2]

So you can deploy multiple cluster within single inventory grouped by galera_cluster_name and setup interconnection by
galera_cluster_members variable.

Examples
--------

Install galera cluster with default settings.

	- hosts: cluster_one
	  vars:
	    - galera_cluster_name: cluster_one
	    - galera_cluster_members: [10.0.0.1, 10.0.0.2]
	  roles:
	    - role: galera

	- hosts: cluster_two
	  vars:
	    - galera_cluster_name: cluster_two
	    - galera_cluster_members: [10.0.1.1, 10.0.1.2]
	  roles:
	    - role: galera

Dependencies
------------

None

License
-------

LGPL

Author Information
------------------

Alexey Medvedchikov, 2GIS, LLC