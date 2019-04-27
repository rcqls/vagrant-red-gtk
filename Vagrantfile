# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
   
  config.vm.box = "bento/debian-9.6-i386"
  config.vm.box_version = "201812.27.0"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  
  if File.exists? "synced_folder.cfg"
    File.read("synced_folder.cfg").strip.split("\n").each do |line|
      src,dest=line.split(":").map{|e| e.strip}
      # puts src + " => " + dest
      config.vm.synced_folder src, dest
    end
  end

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  config.vm.provider :virtualbox do |vb|
     # Use VBoxManage to customize the VM. For example to change memory:
     vb.memory = 2048
     vb.name = "red-gtk-dev-debian"
     #vb.gui = true
   end

   config.ssh.extra_args="-Y"
   config.ssh.forward_agent=true
   config.ssh.forward_x11=true
  
  # View the documentation for the provider you're using for more
  # information on available options.
  config.vm.provision :shell, :inline => <<-SHELL
    apt-get update && apt-get install -y wget && apt-get install -y git
    apt-get install -y libc6 libcurl3 
    apt-get install -y libgtk-3.0 #libelementary2
    apt-get install -y dbus-x11  xauth
    mkdir -p /var/run/dbus
  SHELL
  config.vm.provision :shell, :privileged => false, :inline => <<-SHELL2
    cd $HOME
    mkdir -p bin
    mkdir -p install
    cd $HOME/install
    wget http://www.rebol.com/downloads/v278/rebol-core-278-4-3.tar.gz
    tar xzvf rebol-core-278-4-3.tar.gz
    mv releases/rebol-core/rebol ~/bin
    ## rcqls/red:GTK-dev from now 
    git clone -b GTK-dev https://github.com/rcqls/red
    ## reds for compilation
    git clone https://github.com/rcqls/reds
    ln -s $HOME/install/reds/reds $HOME/bin/reds
    ## code and community
    git clone https://github.com/red/code
    git clone https://github.com/red/community
    git clone --depth 1 https://github.com/ldci/redCV

    cd $HOME/bin
    wget https://toltex.u-ga.fr/users/RCqls/Red/console-view
    chmod u+x rebol
    chmod u+x console-view

    cd $HOME
    echo 'export RED_GTK_DIR="/home/vagrant/install/red"' >> .bash_profile
    echo 'export PATH=~/bin:$PATH' >> .bash_profile
  SHELL2

end
