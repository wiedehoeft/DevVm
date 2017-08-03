Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/xenial64"

  config.vm.provider "virtualbox" do |vb|
     vb.gui = true
     vb.memory = "8192"
  end
  
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get -y upgrade
    sudo apt-get -y install openjdk-8-jdk openjdk-8-demo openjdk-8-doc openjdk-8-jre-headless openjdk-8-source
	sudo apt-get -y install ubuntu-gnome-desktop 
   
    # Install Docker
	# Set german local
	
	# Create own user
	sudo useradd -m -s /bin/bash developer
	echo "developer:developer" |chpasswd
	sudo usermod -aG sudo developer
	
	# Install Guest Additions

  SHELL
end