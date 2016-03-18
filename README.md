jstatd
======

Role installs jstatd daemon on Linux (Debian) based systems with SysVinit service system.
Tested on Ubuntu Server 14.04.04/trusty.
Use jstatd **on development and very low security level environments only**. Never use jstatd on production system, use JMX with authentication support instead.
Role installs:

* creates file /etc/default/jstatd
* creates file /etc/init.d/jstatd
* creates file /etc/jstatd.policy
* registers service jstatd

Requirements
------------

Requires JVM installed at default (ubuntu) path (/usr/bin/java, /usr/bin/jstatd) or change java_home variable (e.g. /opt/java/jdk8). JDK/JRE installation is out of the scope of this role.

Role Variables
--------------
Roles variables along with default values (see defaults/main.yml):

Jstatd home directory (contains bin/jstatd), default Ubuntu with OpenJDK - /usr/bin/java, /usr/bin/jstatd. Change jstatd_home if custom installation of JDK is in use.

	jstatd_home: /usr
	
Jstatd log directory. Jstatd generates very few data or nothing at all. 

	jstatd_log: /var/log/jstatd.log
	
OS user the jstatd is running under.
	
	jstatd_user: root
	
Java policy premissions used to start jstatd. By default All permissions are granted to jstatd.
	
	jstatd_policy_permission: "java.security.AllPermission"
	
Jstatd policy file to use. Default value is jstatd.policy file createad by this Role. Default policy file created by this role cannot be changed, however jstatd can use any other policy file.
	
	jstatd_policy: "/etc/jstatd.policy"

Dependencies
------------

There are no dependencies in the role, however role requires JVM installed on target system. Use any other role suitable for JVM installation.

Example Playbook
----------------
Install role.
requirements.yml (in your playbook):

	src: mvolejnik.jstatd
	name: jstatd
	
Extend role path for .roles in ansible.cfg if you want to place external roles in your playbook but not in (your) "roles" directory. Defined directory must exists.

	roles_path = .roles
	
Install role on command line, using requirements file and folder for external roles:

	ansible-galaxy install -r requirements.yml -p .roles
	
or install into the standard location of Ansible roles (/etc/ansible/roles):

	ansible-galaxy install -r requirements.yml
	
or install without using requriements.yml (if you don't need it in your CVS):

	ansible-galaxy install mvolejnik.jstatd
	
or install role as a part of your playbook as a play (I like this approach, external role becomes part of installation bundle, but you can exclude it form CVS commits):

	- hosts: all
	  tasks:
	    - name: Prepare Ansible host (local) - downloads external roles.
	      local_action: command ./prepare.sh {{ local_dir }}
	      run_once: yes
		
prepeare.sh:

	#!/bin/bash
	ansible-galaxy install -r requirements.yml -p .roles
		
Simple example play:

    - hosts: javaee
      roles:
         - { role: jstatd }

Simple example play not using default java installation directory

    - hosts: javaee
      roles:
         - { role: jstatd, java_home: "/opt/java/jdk8" }

License
-------

BSD, MIT

Author Information
------------------

Michal Volejnik https://github.com/mvolejnik .`
