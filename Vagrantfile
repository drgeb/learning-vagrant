Vagrant::Config.run do |config|
  config.vm.box = "precise64"

    # Necessary for homesick_agent::data_bag
    config.ssh.forward_agent = true

    config.vm.provision :chef_solo do |chef|

      # Once the Vagrant Berkshelf plugin is installed it can be enabled in your Vagrantfile  
      # Seems like this statement is part of Vagrant v1
      #config.berkshelf.enabled = true

      # contains "users" and "ssh_known_hosts" data_bags
      chef.data_bags_path = "data_bags"

      chef.cookbooks_path = ["cookbooks" ]
    
      # stuff that should be in base box
      #    chef.add_recipe "sudo"
      chef.json = {
              'authorization' => {
                  'sudo' => {
                    'groups' => ['admin', 'wheel', 'sysadmin'],
                    'users' => ['testuser', 'vagrant'],
                    'passwordless' => true,
                    'include_sudoers_d' => true,
                   }
               },

      }

      chef.run_list = [
      		      'recipe[sudo]',
      		      ]

      # setup users (from data_bags/users/*.json)
      chef.add_recipe "users::ruby_shadow" # necessary for password shadow support
      chef.add_recipe "users::sysadmins" # creates users and sysadmin group
      chef.add_recipe "users::sysadmin_sudo" # adds %sysadmin group to sudoers

      chef.add_recipe "git"
      # Seems like nginx needs apt to be loaded first!
      chef.add_recipe "apt"
      chef.add_recipe "nginx"

      chef.add_recipe "build-essential" 
      chef.add_recipe "emacs"
      chef.add_recipe "java"

      chef.add_recipe "nmon"
      chef.add_recipe "maven"
      #    chef.add_recipe "ant"
      #    chef.add_recipe "eclipse"
      #    chef.add_recipe "jrules"
      #    chef.add_recipe "chef-sonar"
      #    chef.add_recipe "timezone-ii"
      #    chef.add_recipe "ntp"

      chef.json = {
        :rabbitmq => {
          :enabled_plugins => ["rabbitmq_management"]
        },
	:java => {
	     :install_flavor => "oracle",
	     :java_home => "/opt/myjava",
	     :tarball => "jdk-7u45-linux-x64.tar.gz",
	     :url => "//file/vagrant/install-images/oracle/java/javase/downloads/jdk7-downloads",
	     :oracle => {
	     	       	   "accept_oracle_download_terms" => true
	     }
	}
   }
    end
end