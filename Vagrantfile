Vagrant.configure("2") do |config|
  # All server set
  config.vm.box = "ubuntu/focal64"
  config.vm.box_check_update = true
  config.vm.boot_timeout = 300
  # config.vm.network "public_network", bridge: "bridge0"
  # config.disksize.size = '50GB'
  config.vm.synced_folder '.', '/vagrant', disabled: true
  
  config.vm.define "test1" do |test1|
    test1.vm.hostname = "test1"
    # test1.vm.network "public_network", bridge: "brdige0"
    # test1.vm.network "private_network", ip: "192.168.10.10"
    # test1.vm.disk :disk, size: "100GB", primary: true
    # test1.vm.network "public_network", ip: "192.168.150.50"
    # test1.vm.network "public_network", ip: "192.168.103.11", gateway: "192.168.0.1", dns: "168.126.63.1"
    test1.vm.network :public_network, ip: '192.168.150.50', :netmask => '255.255.0.0', :bridge => 'enp4s0'
    test1.disksize.size = '50GB'
    test1.vm.provider "virtualbox" do |v|
      v.name = "test1"
      v.memory = 2048
      v.cpus = 2
      v.linked_clone = true
      v.gui = false
    end

   test1.vm.provision "file", source: ".", destination: "/tmp/vagrant"
   test1.vm.provision "shell", inline: <<-SHELL
	sudo mv /tmp/vagrant /vagrant
	sudo cp /vagrant/SSH/sshd_config /etc/ssh/sshd_config
	sudo systemctl restart sshd
	sudo apt update
	sudo apt upgrade
   SHELL
  end 
end
