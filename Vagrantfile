# General project settings
#################################

  # IP Address for the host only network, change it to anything you like
  # but please keep it within the IPv4 private network range
  ip_address = "172.22.22.22"

  # The project name is base for directories, hostname and alike
  project_name = "dev"

Vagrant.configure("2") do |config|

  # Use hostonly network with a static IP Address and enable
    # hostmanager so we can have a custom domain for the server
    # by modifying the host machines hosts file
    config.hostmanager.enabled = true
    config.hostmanager.manage_host = true
    config.vm.define project_name do |node|
      node.vm.hostname = project_name + ".local"
      node.vm.network :private_network, ip: ip_address
      node.hostmanager.aliases = [ "www." + project_name + ".local" ]
    end
    config.vm.provision :hostmanager

  # Enable the Puppet provisioner, with will look in manifests
  config.vm.provision :puppet do |puppet|
    puppet.manifests_path = "manifests"
    puppet.manifest_file = "default.pp"
    puppet.module_path = "modules"
  end

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "precise32"

  # Forward guest port 80 to host port 8888 and name mapping
  # config.vm.network :forwarded_port, guest: 80, host: 8888

  config.vm.synced_folder "D:/Lab/", "/vagrant/webroot/", :owner => "www-data"
end
