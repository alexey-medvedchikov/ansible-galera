galera
======

This role configures Galera/MariaDB 5.5 cluster.

Requirements
------------

All requirements are listed in [metadata file](meta/main.yml).

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

	# Nodes with this parameter set to zero will be configured as standalone,
	# i.e. wsrep_cluster_address=gcomm://
	galera_bootstrap: 0

	# Unique Galera cluster identifier
	galera_cluster_name: mycluster

	# Addresses of cluster nodes to connect to
	galera_cluster_members: [10.0.0.1, 10.0.0.2]

	# Setup apt repository sources or not
	galera_setup_repository: yes

	# Install packages or not
	galera_install_packages: yes

	# Install ClusterCheck or not
	galera_install_clustercheck: yes

So you can deploy multiple cluster within single inventory grouped by galera_cluster_name and setup
interconnection by galera_cluster_members variable.

Examples
--------

Install Galera cluster with default settings.

	- hosts: cluster_one
	  vars:
	    - galera_cluster_name: cluster_one
	    - galera_cluster_members: [10.0.0.1, 10.0.0.2]
	  roles:
	    - role: galera
	      become: yes

	- hosts: cluster_two
	  vars:
	    - galera_cluster_name: cluster_two
	    - galera_cluster_members: [10.0.1.1, 10.0.1.2]
	  roles:
	    - role: galera
	      become: yes

Example inventory file:

	[cluster_one]
	10.0.0.1 galera_bootstrap=1
	10.0.0.2

	[cluster_two]
	10.0.1.1 galera_bootstrap=1
	10.0.1.2

Helpers
-------

Variable shows current node state:

	mysql -e "SHOW STATUS LIKE 'wsrep_local_state_comment';"

Variable shows if node is ready to accept queries:

	mysql -e "SHOW STATUS LIKE 'wsrep_ready';"

Variable shows if the node is connected to the cluster:

	mysql -e "SHOW STATUS LIKE 'wsrep_connected';"

Variable shows status of the cluster component:

	mysql -e "SHOW STATUS LIKE 'wsrep_cluster_status';"

Dependencies
------------

None

License
-------

LGPL

Author Information
------------------

- Alexey Medvedchikov, 2GIS, LLC
- Sergey Antipov, 2GIS, LLC
