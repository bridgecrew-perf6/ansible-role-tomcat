# ansible-role-tomcat

### Deploy instanciated tomcat.
Can be tried with pragmatiker/ansible-role-xwiki for fun
### At the Moment it has tasks to:
- [x] Download tar.gz & extract lib/bin (catalina_home) to /opt/tomcat/apache-tomcat-{{tomcat_version}} 
- [x] Installs Java
- [x] Test run catalina.jar, output Tomcat and Java version
- [x] Create instance catalina_base (lib,bin,conf, etc.) under  /opt/tomcat/{{software}}-{{stage}}
- [x] Create configs setenv.sh, server.xml, logging.properties, logrotate.conf from templates
- [x] Create & enable systemd service unit
- [x] See if I can make it loop through multiple Instances or resort to multiple plays
 
### ToDo:
- [ ] eat cookies


### Example group_vars
```
---
basedir: /opt/tomcat
software: xwiki
xwiki_version: 11.10.12
stage: qs
tomcat_version: 8.5.61
tomcat_instances:
  - instance: acme
    http_port: 8080
    shutdown_port: 8005
    db_passwd: CTS9K4XKfO
    stage: dev
  - instance: umbrellacorp
    http_port: 9080
    shutdown_port: 9005
    db_passwd: a08tg6zz81
    stage: viral
  - instance: starkindustries
    http_port: 10080
    shutdown_port: 10005
    db_passwd: E4G144kL6t
  - instance: nebula
    http_port: 11080
    shutdown_port: 11005
    db_passwd: I80BuBXzh6
 ```
 
### Example Playbook 
```
---
- name: Setup my xwiki
  hosts: xwiki_qs
  gather_facts: yes
  become: yes
  pre_tasks:
    - name: Update apt cache.
      apt: update_cache=true cache_valid_time=600
      when: ansible_os_family == 'Debian'
    - name: Ensure unip is installed
      package: name=unzip state=present
  roles:
    - role: ansible-role-tomcat
