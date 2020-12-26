# ansible-role-tomcat

### Deploy instanciated tomcat.
### At the Moment it has tasks to:
- [x] Download tar.gz & extract lib/bin (catalina_home) to /opt/tomcat/apache-tomcat-{{tomcat_version}} 
- [x] Installs Java (zypper only atm)
- [x] Test run catalina.jar, output Tomcat and Java version
- [x] Create instance catalina_base (lib,bin,conf, etc.) under  /opt/tomcat/{{software}}-{{stage}}
- [x] Create configs setenv.sh, server.xml, logging.properties, logrotate.conf from templates
- [x] Create & enable systemd service unit
 
### ToDo:
- [ ] Create a role for xwiki or another application that uses Tomcat
- [ ] Deploy WAR File in the created instance and smile :)
- [ ] See if I can make it loop through multiple Instances or resort to multiple plays
 
### Example Playbook 
### Uses Vars software (xWiki), stage (dev/qs/prod), tomcat_version, shutdown_port, http_port
```
### Example Playbook 
```
- name: Setup my xwiki
  hosts: server
  gather_facts: yes
  become: yes
  vars:
    basedir: /opt/tomcat
    software: xwiki
    stage: qs
    tomcat_version: 8.5.61
    xwiki_version: 11.10.12
    shutdown_port: 8005
    http_port: 8080
  roles:
    - role: ansible-role-tomcat
    - role: ansible-role-xwiki
