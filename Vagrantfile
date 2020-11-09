# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.hostname = "ubuntu-docker"

  for i in 55000..55050
    config.vm.network "forwarded_port", guest: i, host: i
  end
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  config.vm.synced_folder "~/Projects", "/home/vagrant/Projects", owner: "vagrant", group: "vagrant"

  config.vm.provider "virtualbox" do |vb|
    vb.name = "ubuntu-docker"
    vb.memory = "1024"
    # vb.gui = true
  end
  
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update

    apt-get install -y \
      apt-transport-https \
      ca-certificates \
      curl \
      gnupg-agent \
      software-properties-common
    
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -

    add-apt-repository -y \
      "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
      $(lsb_release -cs) \
      stable"

    apt-get update

    apt-get install -y \
      docker-ce \
      docker-ce-cli \
      containerd.io
    
    curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
    chmod +x /usr/local/bin/docker-compose
    
    adduser vagrant docker
  SHELL
end
