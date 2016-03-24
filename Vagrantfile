# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    config.ssh.forward_agent = true

    config.vm.box = "ubuntu/trusty64"
    config.vm.box_url = "https://vagrantcloud.com/ubuntu/boxes/trusty64/versions/14.04/providers/virtualbox.box"

    config.vm.network :private_network, ip: "33.33.33.10"

    config.vm.hostname = "shopware5.local"

    config.vm.synced_folder "./ansible", "/ansible"
    #config.vm.synced_folder "./src", "/home/vagrant/www/shopware5", create: true, type: "smb"
    #config.vm.synced_folder "./src", "/home/vagrant/www/shopware5", create: true, type: "nfs"
    config.vm.synced_folder "./src", "/home/vagrant/www/shopware5", create: true;

    config.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--cpus", 4]
        vb.customize ["modifyvm", :id, "--ioapic", "on"]
        vb.customize ["modifyvm", :id, "--memory", 2048]
        vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    end

    config.vm.provision :shell do |sh|
        sh.keep_color = true
        sh.privileged = false
        sh.path = "provision.sh"
        sh.args = "./ansible-tmp /ansible/playbook.yml /vagrant/ansible-inventory"
    end
end
