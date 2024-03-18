 # -*- mode: ruby -*-
 # vi: set ft=ruby :



Vagrant.configure("2") do |config|
    config.vm.box = "generic/debian11"
    config.vm.synced_folder  "./", "/vagrant", create: true, disabled: false

    
    

    config.vm.provider "virtualbox" do |vb|
        vb.memory = "1024"


    end

    config.vm.define "web_php", primary: true do |web|
        web.vm.network "private_network", ip: "192.168.56.6"
    
    end    
      
    config.vm.define "web_rev_proxy", primary: true do |web|
        web.vm.network "private_network", ip: "192.168.56.7"   

        web.vm.provision :file, source: '.vagrant/machines/web_php/virtualbox/private_key', destination: '/home/vagrant/private_key_web_php'
        
        web.vm.provision "ansible_local" do |ansible|
            ansible.playbook = "playbook.yaml"
            ansible.limit = "all"
            ansible.inventory_path = "inventory"
      end
   end      
end 

