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
    sudo wget -O /opt/eclipse-javascript-oxygen.zip https://www.eclipse.org/downloads/download.php?file=/technology/epp/downloads/release/oxygen/R/eclipse-javascript-oxygen-R-win32-x86_64.zip&r=1
    cd /opt/ && sudo unzip eclipse-javascript-oxygen.zip

	# Install Docker
	# Set german local
	# Create own user

  SHELL
end