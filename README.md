# ansible-role-tomcat
Deploy instanciated tomcat
At the Moment it has tasks to:
 * Download tar.gz & extract lib/bin (catalina_home) to /opt/tomcat/apache-tomcat-{{ tomcat_version }} 
 * Installs Java (zypper only atm)
 * Test run 

Need to do: 
 * Take Vars SOFTWARE (like xWiki), STAGE (QS/PROD) 
 * build instance catalina_base (lib,bin,conf, etc.) under  /opt/tomcat/{{ SOFTWARE }}-{{ STAGE }}
 * deploy systemd UNIT File that sets catalina_home & catalina_base

