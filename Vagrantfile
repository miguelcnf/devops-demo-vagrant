# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # use ubuntu/trusty64 as a base image
  config.vm.box = "ubuntu/trusty64"
  # port forward 8080 from guest to host
  config.vm.network "forwarded_port", guest: 8080, host: 8080
  # sync our source directory on the host to /vagrant in the guest
  config.vm.synced_folder ".", "/vagrant"

  # virtualbox configuration
  config.vm.provider "virtualbox" do |vb|
    # set virtual machine memory
    vb.memory = "256"
  end

  # provision and start our hello program in the background
  config.vm.provision "shell", inline: <<-SHELL
    wget -q https://dl.google.com/go/go1.13.1.linux-amd64.tar.gz
    tar -C /usr/local -xzf go1.13.1.linux-amd64.tar.gz
    /usr/local/go/bin/go build -o /usr/bin/hello /vagrant/hello.go
    chmod 755 /usr/bin/hello
    /usr/bin/hello &
  SHELL
end
