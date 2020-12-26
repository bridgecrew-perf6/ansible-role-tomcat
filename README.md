# ansible-role-tomcat
---
Deploy instanciated tomcat.
---

At the Moment it has tasks to:
 * Download tar.gz & extract lib/bin (catalina_home) to /opt/tomcat/apache-tomcat-{{tomcat_version}} 
 * Installs Java (zypper only atm)
 * Test run catalina.jar 
 * Create instance catalina_base (lib,bin,conf, etc.) under  /opt/tomcat/{{software}}-{{stage}}
 * Create configs seten.sh, server.xml, logging.properties, logrotate.conf
 * deploy systemd UNIT File that sets catalina_home & catalina_base
 
ToDo:
 * Create a role for xwiki or another application that uses Tomcat
 * Create tasks for creatiog of database and application configs
 * Deploy WAR File in the created instance and smile :)
 ---
 
 Take Vars software (like xWiki), stage (QS/PROD), tomcat_version, shutdown_port, http_port
 ---
- name: Setup my Tomcat Xwiki Instance
  hosts: server
  gather_facts: yes
  become: yes
  vars:
    software: xwiki
    stage: qs
    tomcat_version: 8.5.61
    shutdown_port: 8005
    http_port: 8080
  roles:
    - role: ansible-role-tomcat


 
