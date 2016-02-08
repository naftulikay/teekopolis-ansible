# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "fedora/fedora-cloud-23"
  config.vm.box_url = "https://download.fedoraproject.org/pub/fedora/linux/releases/23/Cloud/x86_64/Images/Fedora-Cloud-Base-Vagrant-23-20151030.x86_64.vagrant-virtualbox.box"

  config.vm.hostname = "ansible"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", type: "dhcp"

  config.vm.provider "virtualbox" do |vb|
  #   # Use VBoxManage to customize the VM. For example to change memory:
    vb.customize ["modifyvm", :id, "--memory", "1024"]
  end

  # get to a sane default
  config.vm.provision "shell", inline: "dnf install -y mate-desktop python-dnf libselinux-python", run: "once"
  # then run ansible
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "vagrant.yml"
    ansible.raw_arguments  = "--ask-vault-pass"
    ansible.sudo = true
  end
end
