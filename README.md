# ansible-role-tomcat

### Deploy instanciated tomcat from group_vars
Has shared CATALINA_HOME for all instances

### At the Moment it has tasks to:
- [x] Download tar.gz & extract lib/bin (catalina_home) to /opt/tomcat/apache-tomcat-{{tomcat_version}} 
- [x] Installs Java
- [x] Test run catalina.jar, output Tomcat and Java version
- [x] Create instance catalina_base (lib,bin,conf, etc.) under  /opt/tomcat/tomcat-{{software}}-{{instance}}-{{stage}}
- [x] Create configs setenv.sh, server.xml, logging.properties, logrotate.conf from templates
- [x] Create & enable systemd service unit
- [x] See if I can make it loop through multiple Instances or resort to multiple plays
 
### ToDo:
- [ ] build a role for xwiki as company :)


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
    tomcat_http_port: 8080
    tomcat_shutdown_port: 8005
    stage: dev
  - instance: umbrellacorp
    tomcat_http_port: 9080
    tomcat_shutdown_port: 9005
    stage: viral
  - instance: starkindustries
    tomcat_http_port: 10080
    tomcat_shutdown_port: 10005
  - instance: nebula
    tomcat_http_port: 11080
    tomcat_shutdown_port: 11005
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
