# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  # Set box type for all machines
  config.vm.box = "bento/ubuntu-16.04" # 16.04 LTS

  # Provision all machines with script
  config.vm.provision "shell", inline: $script, privileged: false

  # Install docker
  config.vm.provision "docker"

  # Server 1
  config.vm.define "s1" do |s1|
      s1.vm.hostname = "s1"
      # Provision machine as server node
      config.vm.provision "shell", path: "start-server.sh"
      config.vm.provision "file", source: "./nomad/server1.hcl", destination: "$HOME/server1.hcl"
      s1.vm.network "private_network", ip: "172.20.20.10"
      # Expose Nomad UI port to localhost
      config.vm.network "forwarded_port", guest: 4646, host: 4646, auto_correct: true
  end

  # Client 1
  config.vm.define "c1" do |c1|
      c1.vm.hostname = "c1"
      # Provision machine as client node
      config.vm.provision "shell", path: "start-client.sh"
      config.vm.provision "file", source: "./nomad/client1.hcl", destination: "$HOME/client1.hcl"
      c1.vm.network "private_network", ip: "172.20.20.11"
  end

  # Client 2
  config.vm.define "c2" do |c2|
      c2.vm.hostname = "c2"
      # Provision machine as client node
      config.vm.provision "shell", path: "start-client.sh"
      config.vm.provision "file", source: "./nomad/client2.hcl", destination: "$HOME/client2.hcl"
      c2.vm.network "private_network", ip: "172.20.20.12"
  end
end