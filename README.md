# ansible-role-tomcat
Deploy instanciated tomcat
At the Moment it has tasks to:
 * Download tar.gz & extract lib/bin (CATALINA_HOME) to /opt/tomcat/apache-tomcat-{{ TOMCAT_VERSION }} 
 * Installs Java (zypper only atm)
 * Test run 

Need to do: 
 * Take Vars SOFTWARE (like xWiki), STAGE (QS/PROD) 
 * build instance CATALINA_BASE (lib,bin,conf, etc.) under  /opt/tomcat/{{ SOFTWARE }}-{{ STAGE }}
 * deploy systemd UNIT File that sets CATALINA_HOME & CATALINA_BASE

