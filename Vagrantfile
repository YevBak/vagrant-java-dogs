# Vagrantfile for provisioning a Java application VM

Vagrant.configure("2") do |config|

  # Base box - Ubuntu Jammy 22.04
  config.vm.box = "ubuntu/jammy64"

  # Set hostname for the VM
  config.vm.hostname = "java-vm"

  # Synced folder: maps local './vagrant' to '/vagrant' in the VM
  config.vm.synced_folder "./vagrant", "/vagrant"

  # Set up private network with static IP
  config.vm.network "private_network", ip: "192.168.100.100"

  # VirtualBox settings: 2 CPUs, 4096 MB RAM
  config.vm.provider "virtualbox" do |vb|
    vb.cpus = 2
    vb.memory = 4096
  end

  # Provisioner: install OpenJDK 17 via shell
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt update
    sudo apt install -y openjdk-17-jdk
  SHELL

  # Trigger: after `vagrant up`, start Spring Boot app
  config.trigger.after :up do |trigger|
    trigger.info = "Running Spring Boot app..."
    trigger.run = {
      inline: "cd /vagrant && ./gradlew bootRun"
    }
  end

end
