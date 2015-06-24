# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
    config.vm.define "patternlab" do |patternlab|
        patternlab.vm.box = "debian"
        patternlab.vm.box_url = "ftp://ftp.lugons.org/vagrant/debian-8.0-x86_64.box"
        patternlab.vm.hostname = "vagrant.patternlab.local"
        patternlab.vm.network :private_network, ip: "192.168.33.40"

        patternlab.vm.provider "virtualbox" do |vb|
            vb.memory = "1024"
        end

        patternlab.vm.synced_folder "./shared",
            "/var/www/html/",
            :id => "www-root",
            :owner => "vagrant",
            :group => "www-data",
            mount_options: ["dmode=777,fmode=776"]

        patternlab.vm.provision "ansible" do |ansible|
            ansible.playbook = "site.yml"
            ansible.host_key_checking = false
            ansible.groups = {
                "vagrant" => ["patternlab"],
            }
        end
    end
end
