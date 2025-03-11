# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  servers=[
    {
      :hostname => "ansible-control",
      :box => "bento/ubuntu-24.04",
      :box_version=> "202502.21.0",
      :ip => "192.168.56.200",
      :ssh_port => '2235'
    },
    {
      :hostname => "db01",
      :box => "generic/alpine318",
      :box_version=> "4.3.12",
      :ip => "192.168.56.201",
      :ssh_port => '2230'
    },
    {
      :hostname => "web01",
      :box => "generic/alpine318",
      :box_version=> "4.3.12",
      :ip => "192.168.56.202",
      :ssh_port => '2231'
    },
    {
      :hostname => "web02",
      :box => "generic/alpine318",
      :box_version=> "4.3.12",
      :ip => "192.168.56.203",
      :ssh_port => '2232'
    },
    {
      :hostname => "loadbalancer",
      :box => "generic/alpine318",
      :box_version=> "4.3.12",
      :ip => "192.168.56.204",
      :ssh_port => '2233'
    },
    {
      :hostname => "file01",
      :box => "generic/alpine318",
      :box_version=> "4.3.12",
      :ip => "192.168.56.205",
      :ssh_port => '2234'
    }

  ]

  servers.each do |machine|

    config.vm.define machine[:hostname] do |node|
      node.vm.box = machine[:box]
      node.vm.box_version = machine[:box_version] if machine[:box_version]
      node.vm.hostname = machine[:hostname]
    
      node.vm.network :private_network, ip: machine[:ip]
      node.vm.network "forwarded_port", guest: 22, host: machine[:ssh_port], id: "ssh"
      
      node.vm.provider :virtualbox do |v|
        v.customize ["modifyvm", :id, "--memory", 512]
        v.customize ["modifyvm", :id, "--cpus", 1]
        v.customize ["modifyvm", :id, "--name", "A2-#{machine[:hostname]}"]
        # Install ansible on ansible-control node from Vagrantfile
        # if machine[:hostname] == "ansible-control"
        #   node.vm.provision "shell", inline: <<-SHELL
        #     echo "Running apt update on ansible-control..."
        #     sudo apt update -y
        #     echo "Running apt install ansible on ansible-control..."
        #     sudo apt install -y ansible
        #   SHELL
        # end
      end
    end
  end

end