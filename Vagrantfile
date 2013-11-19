# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.ssh.username = "vagrant"
  config.ssh.private_key_path = File.expand_path("~/.vagrant.d/insecure_private_key")
  # config.vm.network :public_network
  # config.ssh.forward_agent = true
  
  config.vm.provider :virtualbox do |virtualbox|
    virtualbox.customize ["modifyvm", :id, "--memory", 512]
  end

  config.vm.define :wordpress do |node|
    node.vm.box = "ringtale64"
    node.vm.box_url = "http://cloud-images.ubuntu.com/vagrant/raring/current/raring-server-cloudimg-amd64-vagrant-disk1.box"
    node.vm.hostname = "wordpress.dev"
    node.vm.network :forwarded_port, guest: 80, host: 8080
    node.vm.network :private_network, ip: "192.168.111.222"
    node.vm.provision :ansible do |ansible|
      ansible.playbook = "site.yml"
      ansible.host_key_checking = "false"
      ansible.inventory_file = "hosts"
      #ansible.verbose = "v"
    end
  end

end