# -*- mode: ruby -*-
# vi: set ft=ruby :

#Vagrant.require_plugin "vagrant-berkshelf"
#Vagrant.require_plugin "vagrant-omnibus"

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  # config.vm.box = "precise64-ruby-1.9.3-p194"
  config.vm.box = "precise64"

  # The url from where the 'config.vm.box' box will be fetched if it
  # doesn't already exist on the user's system.
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  # DRGEB
  # To change the hostname of the birtual environment
  config.vm.hostname = "usingBerkshelf"
  config.berkshelf.enabled = true

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  config.vm.network :forwarded_port, guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network :private_network, ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network :public_network

  # If true, then any SSH connections made will enable agent forwarding.
  # Default value: false
  # config.ssh.forward_agent = true

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  config.vm.synced_folder "../install_images", "/install_images"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider :virtualbox do |vb|
  #   # Don't boot with headless mode
  vb.gui = true
  #
  #   # Use VBoxManage to customize the VM. For example to change memory:
  #   vb.customize ["modifyvm", :id, "--memory", "1024"]
  end
  #
  # View the documentation for the provider you're using for more
  # information on available options.

  # Enable provisioning with Puppet stand alone.  Puppet manifests
  # are contained in a directory path relative to this Vagrantfile.
  # You will need to create the manifests directory and a manifest in
  # the file base.pp in the manifests_path directory.
  #
  # An example Puppet manifest to provision the message of the day:
  #
  # # group { "puppet":
  # #   ensure => "present",
  # # }
  # #
  # # File { owner => 0, group => 0, mode => 0644 }
  # #
  # # file { '/etc/motd':
  # #   content => "Welcome to your Vagrant-built virtual machine!
  # #               Managed by Puppet.\n"
  # # }
  #
  # config.vm.provision :puppet do |puppet|
  #   puppet.manifests_path = "manifests"
  #   puppet.manifest_file  = "site.pp"
  # end

  config.vm.provision :chef_solo do |chef|
       # this provision block upgrades the Chef Client before the real 
       # Chef run starts
#       chef.log_level      = :debug
       chef.add_recipe "chef-client::upgrade"

       # Highly recommended to keep apt packages metadata in sync and
       # be able to use apt mirrors.
       # Put recipe[apt] first in the run list. If you have other recipes that you want to use to configure how apt behaves, like new sources, notify the execute resource to run
       chef.add_recipe "apt"
       chef.json = { 
    	        	"apt" => {
		     	     "compiletime" => true,
			     "periodic_update_min_delay" => 8640
			     }
		  }
  end


  # Enable provisioning with chef solo, specifying a cookbooks path, roles
  # path, and data_bags path (all relative to this Vagrantfile), and adding
  # some recipes and/or roles.
  #
  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = ["cookbooks" ]
    chef.roles_path = [ "roles" ]
    chef.data_bags_path = [ "data_bags" ]

    chef.log_level      = :debug

    chef.add_role "base"
    chef.add_role "performance"
    chef.add_role "developer"
 
    # stuff that should be in base box
#    chef.add_recipe "sudo"
#    chef.json = {
#            'authorization' => {
#                'sudo' => {
#                  'groups' => ['admin', 'wheel', 'sysadmin'],
#                  'users' => ['testuser', 'vagrant'],
#                  'passwordless' => true,
#                  'include_sudoers_d' => true,
#                 }
#             },
#    }

    # setup users (from data_bags/users/*.json)
    #    chef.add_recipe "users::ruby_shadow" # necessary for password shadow support
    chef.add_recipe "chef-solo-search"
#    chef.add_recipe "users::default"
#    chef.add_recipe "users::sysadmins" # creates users and sysadmin group
#    chef.add_recipe "users::sysadmin_sudo" # adds %sysadmin group to sudoers

     
     chef.add_recipe "java"
     chef.add_recipe "magic_java"

     chef.json = {
        :rabbitmq => {
          :enabled_plugins => ["rabbitmq_management"]
        },
	:java => {
	     :install_flavor => "oracle",
	     :java_home => "/opt/myjava",
	     :tarball => "jdk-7u45-linux-x64.tar.gz",
	     :url => "//file/install_images/oracle/java/javase/downloads/jdk7-downloads",
	     :oracle => {
	     	       	   "accept_oracle_download_terms" => true
	     }
	}
   }

#    chef.add_recipe "hostsfile"
#    chef.json = {
#	'hostsfile' => {
#         '10.10.10.10' => 'rabbit2'
#        }
#    }

   chef.add_recipe "emacs"

   chef.add_recipe "apache2"
   chef.add_recipe "git"
   chef.add_recipe "maven"
   chef.add_recipe "openssl"
   # chef.add_recipe "mysql"
   # chef.add_recipe "rabbitmq"
  ##  chef.add_recipe "chef-oracle-xe"
   chef.add_recipe "logwatch"
  ##  chef.add_recipe "nginx"
   chef.add_recipe "tomcat"
  ##  chef.add_recipe "tomcat6_init_script"
  ##  chef.add_recipe "chef-ubuntu-desktop"
  #  chef.add_recipe "chef-android-sdk"
  #  chef.add_role "web"

     # You may also specify custom JSON attributes:
#    chef.json = { :mysql_password => "foo" }

  end

  # ANDROID STUFF USING A SHELL SCRIPT
  config.vm.provision "shell", inline: "echo Installing Android ADT bundle and NDK..."
  config.vm.provision "shell", path: "provision.sh"
  config.vm.provision "shell", inline: "echo Installation complete"

  # Enable provisioning with chef server, specifying the chef server URL,
  # and the path to the validation key (relative to this Vagrantfile).
  #
  # The Opscode Platform uses HTTPS. Su<bstitute your organization for
  # ORGNAME in the URL and validation key.
  #
  # If you have your own Chef Server, use the appropriate URL, which may be
  # HTTP instead of HTTPS depending on your configuration. Also change the
  # validation key to validation.pem.
  #
  # config.vm.provision :chef_client do |chef|
  #   chef.chef_server_url = "https://api.opscode.com/organizations/ORGNAME"
  #   chef.validation_key_path = "ORGNAME-validator.pem"
  # end
  #
  # If you're using the Opscode platform, your validator client is
  # ORGNAME-validator, replacing ORGNAME with your organization name.
  #
  # If you have your own Chef Server, the default validation client name is
  # chef-validator, unless you changed the configuration.
  #
  #   chef.validation_client_name = "ORGNAME-validator"

  # ... other configuration
  config.vm.provision "shell", inline: "echo hello"

end
