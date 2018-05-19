### configuration parameters  ###
VIRTUALBOX_VERSION = "5.2.12" ### TODO: maybe we could determine from Host_OS this?
### /configuration parameters ###

Vagrant.require_version ">= 1.9.0"  
Vagrant.configure("2") do |config|

  config.vm.box = "fedora/25-cloud-base"
 
  config.vm.provider "virtualbox" do |vb|
     vb.gui = true
     vb.memory = "8192"
  end
  
  config.vm.provision "shell", inline: <<-SHELL
    sudo dnf -y update
    sudo dnf -y install java-1.8.0-openjdk-devel
    sudo dnf -y install maven
    sudo dnf -y install gradle
    sudo dnf -y install git git-gui
    sudo dnf -y install dkms
    sudo dnf -y install firefox
    sudo dnf -y install gcc
    sudo dnf -y install unzip
    sudo dnf -y install kernel-devel
    
    # Install Desktop
    sudo dnf -y install @xfce-desktop-environment
    sudo systemctl set-default graphical.target
    rm '/etc/systemd/system/default.target'
    ln -s '/usr/lib/systemd/system/graphical.target' '/etc/systemd/system/default.target'

    # Install chrome (got from epel-release)
    sudo dnf -y install chromium
    
    # Install Visual Studio Code
    sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
    sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
    sudo yum -y install code
    
    # Install Docker (see https://docs.docker.com/engine/installation/linux/docker-ce/centos/#install-using-the-repository) 
    dnf -y install dnf-plugins-core
    sudo dnf config-manager --set-enabled docker-ce-edge
    sudo dnf config-manager --add-repo https://download.docker.com/linux/fedora/docker-ce.repo
    sudo dnf config-manager --set-enabled docker-ce-test
    sudo dnf config-manager --set-disabled docker-ce-edge
    sudo dnf -y install docker-ce
	sudo systemctl start docker

    # Install current Nodejs server (see https://nodejs.org/en/download/package-manager/)
    curl --silent --location https://rpm.nodesource.com/setup_8.x | sudo -E bash -
    sudo dnf -y install nodejs

    # Install Ruby and Jekyll for blogposts at github.io (see https://jekyllrb.com/docs/installation/)
    gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
    \curl -sSL https://get.rvm.io | sudo bash -s stable --ruby
    gem install jekyll

    # Set german local
	  localectl set-keymap de
    
    # Create own user
    sudo useradd -m -s /bin/bash developer
    echo "developer:developer" |chpasswd
    sudo usermod -aG wheel developer

    # Install Guest Additions (TODO: only install when not existing)
    echo export KERN_DIR=/usr/src/kernels/`uname -r` >> ~/.bashrc
    source ~/.bashrc     # to set the variable in your current shell
    wget http://download.virtualbox.org/virtualbox/#{VIRTUALBOX_VERSION}/VBoxGuestAdditions_#{VIRTUALBOX_VERSION}.iso
    sudo mkdir /media/VBoxGuestAdditions
    sudo mount -o loop,ro VBoxGuestAdditions_#{VIRTUALBOX_VERSION}.iso /media/VBoxGuestAdditions
    sudo sh /media/VBoxGuestAdditions/VBoxLinuxAdditions.run
    rm VBoxGuestAdditions_#{VIRTUALBOX_VERSION}.iso
    sudo umount /media/VBoxGuestAdditions
    sudo rmdir /media/VBoxGuestAdditions

	
    #install eclipse
    sudo dnf -y install eclipse

	# Install openjdk9 (https://omajid.wordpress.com/2016/10/04/openjdk-9-for-fedoraepel/)
    sudo dnf -y copr enable omajid/openjdk9
    sudo dnf -y install java-9-openjdk-devel

    ## Open Issues
    # Install citrix Receiver    
    # Shared folder einrichten

  SHELL
end
