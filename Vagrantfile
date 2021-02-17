# -*- mode: ruby -*-
# vi: set ft=ruby :


$script = <<SCRIPT
  echo "----------------Updating and Upgarding System"
  sudo apt-get update > /dev/null
  sudo apt-get upgrade -y > /dev/null

  echo "----------------Installing necessary packages"
  sudo apt-get install cmake libusb-dev libusb-1.0.0-dev build-essential autoconf \
       cutecom git binutils-arm-none-eabi gcc-arm-none-eabi libgtk-3-0 -y > /dev/null 2> /dev/null

  echo "----------------Setup Library"
  mkdir /home/vagrant/opt
  mkdir /home/vagrant/opt/STM32CubeF4
  git clone https://github.com/STMicroelectronics/STM32CubeF4 /home/vagrant/opt/STM32CubeF4 2> /dev/null
  chown -R vagrant /home/vagrant/opt/STM32CubeF4

  echo "----------------Install flash-tool"
  sudo apt-get install rpm pkg-config debhelper -y > /dev/null 2> /dev/null
  mkdir /tmp/stlink
  git clone https://github.com/texane/stlink /tmp/stlink > /dev/null 2> /dev/null
  chown -R vagrant /tmp/stlink
  runuser -l vagrant -c "cd /tmp/stlink && make clean" > /dev/null
  runuser -l vagrant -c "cd /tmp/stlink && make package" > /dev/null 2> /dev/null
  dpkg -i /tmp/stlink/build/Release/dist/stlink*.deb > /dev/null
  ldconfig

  echo "----------------BORKS Manifesto"
  mkdir /home/vagrant/stm32f4-template
  git clone https://github.com/mborko/stm32f4-template /home/vagrant/stm32f4-template > /dev/null 2> /dev/null
  chown -R vagrant /home/vagrant/stm32f4-template
  runuser -l vagrant -c 'cd /home/vagrant/stm32f4-template && make clean' > /dev/null
  runuser -l vagrant -c 'cd /home/vagrant/stm32f4-template && make' > /dev/null 2> /dev/null

  echo "----------------openstm installation"
  if test -f "/home/vagrant/workspace/openstm.tar" ; then
    sudo apt-get install default-jdk -y > /dev/null 2> /dev/null
    tar -xf /home/vagrant/workspace/openstm.tar -C /tmp/
    chown -R vagrant /tmp/openstm
    runuser -l vagrant -c '/tmp/openstm/install_sw4stm32_linux_64bits-v2.9.run /tmp/openstm/auto-install.xml' > /dev/null 2> /dev/null
    echo 'bash /home/vagrant/Ac6/SystemWorkbench/eclipse' > /home/vagrant/eclipse
    chmod 755 /home/vagrant/eclipse 
    chown vagrant /home/vagrant/eclipse 
  else
    echo "----------------openstm.tar not found in workspace dir ABORTED"
  fi
  
SCRIPT

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|

  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
    v.cpus = 1
  end
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "ubuntu/xenial64"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  config.vm.synced_folder "./workspace", "/home/vagrant/workspace", create: true

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  config.ssh.forward_agent = true
  config.ssh.forward_x11 = true

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
  config.vm.provision "shell", inline: $script
end
