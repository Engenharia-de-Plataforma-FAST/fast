Vagrant.configure("2") do |config|
  # Configuração da primeira VM
  config.vm.define "vm1" do |vm1|
    vm1.vm.box = "bento/ubuntu-22.04"
    vm1.vm.network "public_network", ip: "192.168.0.201", bridge: "Intel(R) I211 Gigabit Network Connection"
    vm1.vm.provider "virtualbox" do |vb1|
      vb1.memory = 2048
      vb1.cpus = 1
    end
    vm1.vm.hostname = "lab-vm1"
    # Shell provisioner para instalar o Docker e iniciar o Swarm
    vm1.vm.provision "shell", inline: <<-SHELL
      # Instalação do Docker
      sudo apt-get update
      sudo apt-get install -y docker.io

      # Inicia o Docker Swarm
      #sudo docker swarm init --advertise-addr enp0s3
    SHELL
  end

  # Configuração da segunda VM
  config.vm.define "vm2" do |vm2|
    vm2.vm.box = "bento/ubuntu-22.04"
    vm2.vm.network "public_network", ip: "192.168.0.202", bridge: "Intel(R) I211 Gigabit Network Connection"
    vm2.vm.provider "virtualbox" do |vb2|
      vb2.memory = 2048
      vb2.cpus = 1
    end
    vm2.vm.hostname = "lab-vm2"
    # Shell provisioner para instalar o Docker
    vm2.vm.provision "shell", inline: <<-SHELL
      # Instalação do Docker
      sudo apt-get update
      sudo apt-get install -y docker.io
    SHELL
  end

  # Configuração da terceira VM
  config.vm.define "vm3" do |vm3|
    vm3.vm.box = "bento/ubuntu-22.04"
    vm3.vm.network "public_network", ip: "192.168.0.203", bridge: "Intel(R) I211 Gigabit Network Connection"
    vm3.vm.provider "virtualbox" do |vb3|
      vb3.memory = 2048
      vb3.cpus = 1
    end
    vm3.vm.hostname = "lab-vm3"
    # Shell provisioner para instalar o Docker
    vm3.vm.provision "shell", inline: <<-SHELL
      # Instalação do Docker
      sudo apt-get update
      sudo apt-get install -y docker.io
    SHELL

  end
  # Configure the /etc/hosts file for each VM
  config.vm.provision "shell", inline: <<-SHELL
    # Update /etc/hosts with entries for other VMs
    echo "192.168.0.201 lab-vm1" | sudo tee -a /etc/hosts
    echo "192.168.0.202 lab-vm2" | sudo tee -a /etc/hosts
    echo "192.168.0.203 lab-vm3" | sudo tee -a /etc/hosts
  SHELL
  config.vm.synced_folder ".", "/vagrant", type: "virtualbox"
  end
  