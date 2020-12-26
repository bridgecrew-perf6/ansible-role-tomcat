# ansible-role-tomcat
---
Deploy instanciated tomcat.
---

At the Moment it has tasks to:
---
- [x] Download tar.gz & extract lib/bin (catalina_home) to /opt/tomcat/apache-tomcat-{{tomcat_version}} 
- [x] Installs Java (zypper only atm)
- [x] Test run catalina.jar 
- [x] Create instance catalina_base (lib,bin,conf, etc.) under  /opt/tomcat/{{software}}-{{stage}}
- [x] Create configs seten.sh, server.xml, logging.properties, logrotate.conf
- [x] deploy systemd UNIT File that sets catalina_home & catalina_base
 
ToDo:
---
- [x] Create a role for xwiki or another application that uses Tomcat
- [x] Create tasks for creatiog of database and application configs
- [x] Deploy WAR File in the created instance and smile :)

 
 Take Vars software (like xWiki), stage (QS/PROD), tomcat_version, shutdown_port, http_port
 ---
 ```
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


 
