Role Name
=========

Role instal jstatd daemon on Linux (Debian) based systems with SysVinit service system.
Tested on Ubuntu Server 14.04.04/trusty.
Use jstatd **only on development and very low security environment**. Never use jstatd on production system, use JMX and authentication instead.

Requirements
------------

Requires JVM installed at default path /opt/java/jdk8 or change java_home variable. 

Role Variables
--------------
Roles variables along with default values (see defaults/main.yml):

Jstatd home directory (contains bin/jstatd). Set up to JAVA_HOME if custom installation of JDK is in use.

	jstatd_home: /usr
	
Jstatd log directory. Jstatd generated very few data or nothing at all. 

	jstatd_log: /var/log/jstatd.log
	
OS user the jstatd is running under.	
	
	jstatd_user: root
	
Java policy premissions used to start jstatd. By default All permissions are granted to jstatd.
	
	jstatd_policy_permission: "java.security.AllPermission"
	
Jstatd policy file to use. Default value is jstatd.policy file createad by this Role. Default policy file created by this role cannot be changed, however jstatd can use any other policy file.
	
	jstatd_policy: "/etc/jstatd.policy"

Dependencies
------------

No dependencies in the role, however requires JVM installed on target system. Used any other role suitable for JVM installation.

Example Playbook
----------------

Simple example play:

    - hosts: javaee
      roles:
         - { role: mvolejnik.jstatd }

Simple example play not using default java installation directory

    - hosts: javaee
      roles:
         - { role: mvolejnik.jstatd, java_home: "/usr/java/jdk8" }

License
-------

BSD, MIT

Author Information
------------------

Michal Volejni.
