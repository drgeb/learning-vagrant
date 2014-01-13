Vagrant::Config.run do |config|
  config.vm.box = "precise64"

  # Necessary for homesick_agent::data_bag
  config.ssh.forward_agent = true

  config.vm.provision :chef_solo do |chef|

    # contains "users" and "ssh_known_hosts" databags
    chef.data_bags_path = "databags"

    chef.cookbooks_path = ["cookbooks" ]

    # stuff that should be in base box
    #  chef.add_recipe "git"

    # setup users (from data_bags/users/*.json)
    chef.add_recipe "users::ruby_shadow" # necessary for password shadow support
    chef.add_recipe "users::sysadmins" # creates users and sysadmin group
    chef.add_recipe "users::sysadmin_sudo" # adds %sysadmin group to sudoers

  end
end