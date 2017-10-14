Vagrant.configure(2) do |config|

  config.vm.box = "centos/7"

  config.vm.provider "virtualbox" do |vb|
     vb.gui = true
     vb.memory = "8192"
  end
  
  config.vm.provision "shell", inline: <<-SHELL
    sudo yum update
    sudo yum -y install java-1.8.0-openjdk-devel wget epel-release kernel-devel gcc dkms firefox
    sudo yum -y groupinstall "X Window system" xfce
    sudo systemctl set-default graphical.target
    rm '/etc/systemd/system/default.target'
    ln -s '/usr/lib/systemd/system/graphical.target' '/etc/systemd/system/default.target'
    
    # Install Visual Studio Code
    sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
    sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
    sudo yum -y install code

    # Install Eclipse
    # Install Docker
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

    # Install Guest Additions
    echo export KERN_DIR=/usr/src/kernels/`uname -r` >> ~/.bashrc
    source ~/.bashrc     # to set the variable in your current shell
    wget http://download.virtualbox.org/virtualbox/5.1.26/VBoxGuestAdditions_5.1.26.iso
    sudo mkdir /media/VBoxGuestAdditions
    sudo mount -o loop,ro VBoxGuestAdditions_5.1.26.iso /media/VBoxGuestAdditions
    sudo sh /media/VBoxGuestAdditions/VBoxLinuxAdditions.run
    rm VBoxGuestAdditions_5.1.26.iso
    sudo umount /media/VBoxGuestAdditions
    sudo rmdir /media/VBoxGuestAdditions

  SHELL
end