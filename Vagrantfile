# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|

  config.vm.box = "hashicorp/bionic64"
  config.vm.provider "virtualbox" do |v|
    v.name = "VM to flash firmware into Arduino"
    v.customize ["modifyvm", :id, "--usb", "on"]
    v.customize ["modifyvm", :id, "--usbehci", "on"]
    # Please rewrite according to your environment. VID/PID is required

    # Keyboard in normal mode
    v.customize ["usbfilter", "add", "0",
                 "--target", :id,
                 "--name", "Redox_wireless",
                 "--remote", "no"]

    # Keyboard in boot/edit mode
    v.customize ["usbfilter", "add", "1",
                 "--target", :id,
                 "--name", "Arduino Micro",
                 "--vendorid", "9025",
                 "--productid", "55",
                 "--remote", "no"]
  end

  # I used local qmk_firmware repository.
  # Please rewrite according to your environment.
  config.vm.synced_folder "/Users/mrobins1/Work/qmk_firmware", "/qmk_firmware"
  config.vbguest.auto_update = true

  # Install build tools
  config.vm.provision "shell", privileged: false, inline: <<-SHELL
    sudo apt-get update
    sudo apt-get install -y python3-pip avrdude
    /qmk_firmware/util/qmk_install.sh
   SHELL

   # Occasionally I get warnings about clock drift without this
   config.vm.provision :shell, :inline => "sudo rm /etc/localtime && sudo ln -s /usr/share/zoneinfo/Pacific/Auckland /etc/localtime", run: "always"
end
