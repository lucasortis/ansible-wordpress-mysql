Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/bionic64"

    config.vm.provider "virtualbox" do |vb|
        vb.memory = 512
        vb.cpus = 1
    end

        config.vm.define "wordpress" do |wordpress|
            wordpress.vm.provider "virtualbox" do |vb|
                vb.memory = 1024
                vb.cpus = 1
                vb.name = "ubuntu_bionic_wordpress"
            end

            #wordpress.vm.network "forwarded_port", guest: 8888, host: 8888
            wordpress.vm.network "public_network", ip: "192.168.15.11"

            wordpress.vm.synced_folder ".", "/vagrant", disabled: true
            wordpress.vm.synced_folder "./configs", "/configs"  
        end 
        
        config.vm.define "mysqlserver" do |mysqlserver|
            mysqlserver.vm.provider "virtualbox" do |vb|
                vb.name = "ubuntu_bionic_mysqlserver"
            end

            #mysqlserver.vm.network "forwarded_port", guest: 80, host: 8089 
            mysqlserver.vm.network "public_network", ip: "192.168.15.10"
            
            mysqlserver.vm.synced_folder ".", "/vagrant", disabled: true
            mysqlserver.vm.synced_folder "./configs", "/configs"    
        end        

        config.vm.provision "ansible" do |ansible|
            ansible.playbook = "./configs/ansible/playbook.yaml"
        end

end