# -*- mode: ruby -*- 222
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    # Base VM OS configuration
    config.vm.box = "centos/7"
    config.vm.box_version = "2004.01"
    config.vm.box_check_update = false

    config.vm.provider :virtualbox do |v|
        v.memory = 512
        v.cpus = 1
    end

    # Define two VMs with static private IP adresses.
    boxes = [
        {
            :name => "web",
            :ip => "192.168.56.10",
        },
		{
			:name => "log",
			:ip => "192.168.56.15",
		}
	]

	boxes.each do |opts|
		config.vm.define opts[:name] do |config| 
			config.vm.hostname = opts[:name] 
			config.vm.network "private_network", ip: opts[:ip]
			if opts[:name] == boxes.last[:name]
			config.vm.provision "ansible" do |ansible| 
			ansible.playbook = "epel.yml" 
			ansible.inventory_path = "hosts" 
			ansible.host_key_checking = "false" 
			ansible.limit = "all"
			end 
		end
	end 
end

	# Provision each of the VMS.
#	boxes.each do |opts|
#		config.vm.define opts[:name] do |config|
#			config.vm.hostname = opts[:name]
#			config.vm.network "private_network", ip: opts[:ip]
#		    
#		    config.vm.provision "shell", inline: <<-SHELL
#		    sudo -i
 #           yum update
  #          yum install -y nano
#			yum install -y mc
 #           yum install -y tzdata
#			timedatectl set-timezone Asia/Krasnoyarsk
#			systemctl restart chronyd
#			systemctl status chronyd
#			timedatectl
 #           SHELL
#		end
#	end
end
