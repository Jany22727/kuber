Vagrant.configure("2") do |config|
  config.vm.box = "sbeliakou/centos"
  config.vm.network :private_network, ip: "192.168.56.15"

  config.vm.hostname = "kub-box.playpit"
  config.vm.network "forwarded_port", guest: 80, host: 80

  config.ssh.insert_key = false
  config.vm.provider "virtualbox" do |vb|
    vb.name = "kub-box.playpit"
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ["modifyvm", :id, "--cpuexecutioncap", "30"]
    vb.memory = "2560"
  end

  config.vm.provision "shell", inline: <<-SHELL
    yum update -y
    yum install -y wget git vim
    
    # Disabling SWAP
    swapoff -a
    sed -i '/swap/d' /etc/fstab
    
  SHELL
end

