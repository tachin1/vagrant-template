# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|
  config.vagrant.plugins = ["vagrant-vbguest"]
  config.vm.box = "centos/stream8"
  config.vm.vbox_check_update = true
  config.vbguest.installer_options = { allow_kernel_upgrade: true }
  config.vm.define "ansible" do |ansible|
    ansible.vm.synced_folder ".", "/vagrant", automount: true, type: "virtualbox"
    ansible.vm.hostname = "ansible"
    ansible.vm.network "private_network", ip: "10.0.0.1"
    ansible.vm.provider "virtualbox" do |vb|
      vb.name = "ansible"
      vb.gui = false
      vb.cpu = 2
      vb.memory "2048"
    end
    ansible.vm.provision "shell", inline: <<-SHELL
    yum install -y --nogpgcheck epel-release
    yum install -y --nogpgcheck git vim python3 python3-pip
    python3 -m pip install --upgrade pip
    pip3 install ansible==2.8.5
    pip3 install jinja2 --upgrade
    su - -c '/usr/bin/git config --global color.ui true' vagrant
    SHELL
  end
end