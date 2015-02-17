# -*- mode: ruby -*-
# vi: set ft=ruby :

# ==============================================================
#  Notes:
#
#  This Vagrantfile requires the hostmanager plugin. To install:
#    > vagrant plugin install vagrant-hostmanager
#  
#  https://github.com/smdahlen/vagrant-hostmanager
#
# ==============================================================

# Vagrantfile API/syntax version.
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # CentOS Vagrant box for for VirtualBox. Provided by PuppetLabs.
  config.vm.box = "centos-6.4"
  config.vm.box_url = "http://puppet-vagrant-boxes.puppetlabs.com/centos-64-x64-vbox4210.box"

  #config.vm.network "forwarded_port", guest: 8080, host: 8082
  #config.vm.network "forwarded_port", guest: 9990, host: 9992

  # Hostmanager vagrant plugin edits /etc/hosts for guest vms.
  # This allows network communication via hostname to work between vms.
  #   [vagrant@jboss-01 ~]$ ssh jboss-02
  config.hostmanager.enabled = true

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "common.yml"
  end

  # TODO: consider creating for loop as shown at
  # http://docs.vagrantup.com/v2/vagrantfile/tips.html
  config.vm.define "jboss-01" do |jboss|
    jboss.vm.network "private_network", ip: "172.28.128.101"
    
    jboss.vm.hostname = "jboss-01.vagrant.dev"
    jboss.hostmanager.aliases = %w(jboss-01)
  end

  config.vm.define "jboss-02" do |jboss|
    jboss.vm.network "private_network", ip: "172.28.128.102"

    jboss.vm.hostname = "jboss-02.vagrant.dev"
    jboss.hostmanager.aliases = %w(jboss-02)
  end

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Don't boot with headless mode
  #   vb.gui = true
  #
  #   # Use VBoxManage to customize the VM. For example to change memory:
  #   vb.customize ["modifyvm", :id, "--memory", "1024"]
  # end
  #
  # View the documentation for the provider you're using for more
  # information on available options.

end
