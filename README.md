# ansible-role-tomcat
Deploy instanciated tomcat
At the Moment:
 * Only deploys CATALINA_HOME (lib/bin) under /opt/tomcat/apache-tomcat-{{ TOMCAT_VERSION }} 
 * installs Java (zypper only atm)
 * Makes test run 

Need to do: 
 * Take Vars SOFTWARE (like xWiki), STAGE (QS/PROD) 
 * build instance CATALINA_BASE (lib,bin,conf, etc.) under  /opt/tomcat/xwiki-qs
 * install CATALINA_BASE lib,bin,conf,et. 
 * deploy systemd UNIT File that sets CATALINA_HOME & CATALINA_BASE

