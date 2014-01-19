site :opscode

metadata

#System Configuration
cookbook 'curl'
cookbook 'roles', path: 'cookbooks/roles'

# Use chef-solo-search because This recipe (I am guessing its users cookbook uses search. Chef Solo does not support search unless you install the chef-solo-search cookbook.
cookbook 'chef-solo-search'
cookbook 'users'
cookbook 'timezone-ii'
cookbook 'ntp'
cookbook 'sudo'
cookbook 'nmon', git: 'https://github.com/rpunt/chef-nmon.git'
cookbook 'chef-client', path: '../berkshelf/cookbooks/chef-client'
#cookbook 'chef-ssh-keys',
cookbook 'Ohai'
#cookbook 'hostsfile'
cookbook 'wireshark', path: 'cookbooks/wireshark'
cookbook ' cookbook-certificate', git: 'https://github.com/atomic-penguin/cookbook-certificate'

#System Tools
cookbook 'apt'
cookbook 'build-essential'
cookbook 'emacs'

#Development Tools
cookbook 'openssl'
cookbook 'openssh'
cookbook 'nginx'
cookbook 'java'
cookbook 'git'
cookbook 'ant'
cookbook 'maven'
cookbook 'eclipse', git: 'https://github.com/geocent-cookbooks/eclipse.git'
cookbook 'chef-sonar', git: 'https://github.com/geocent-cookbooks/chef-sonar.git'
cookbook 'jrules' , git: 'https://github.com/geocent-cookbooks/jrules.git'
cookbook 'apache2'
cookbook 'tomcat'
cookbook 'mysql'
cookbook 'rabbitmq'
cookbook 'logwatch'

#cookbook 'jrockit', git:
#cookbook 'weblogic', git: 'https://github.com/geocent-cookbooks/weblogic.git'
#cookbook 'oracle-xe' , git: 'https://github.com/geocent-cookbooks/oracle-xe'

#My Cook Books
cookbook 'magic_java', path: 'cookbooks/magic_java'
