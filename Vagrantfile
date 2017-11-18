# -*- mode: ruby -*-
# vi: set ft=ruby :

phpdev_version      = "master"
phpdev_private_ip     = "192.168.56.139"
phpdev_install_path   = "/opt/lemp"
phpdev_web_dir      = "/vagrant/projects"
phpdev_tmp_path     = "/tmp/build"
phpdev_src_path     = "/usr/local/src"
phpdev_php_version    = "5.6.26"
phpdev_host       = "dev"
phpdev_domain       = "example.com"
phpdev_install_php    = 0
phpdev_install_mysql  = 1
phpdev_install_nginx  = 0
phpdev_baseurl          = "https://coding.net/u/k4100p/p/phpdev/git/raw/#{phpdev_version}"

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "k4100p/centos7"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
   config.vm.network "private_network", ip: "#{phpdev_private_ip}"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"
   config.vm.synced_folder ".", "/vagrant", type: "virtualbox"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
   config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
     vb.memory = "2048"
     vb.cpus = 4
   end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   sudo apt-get update
  #   sudo apt-get install -y apache2
  # config.vm.provision "file", source: "vagrant_provision/build.sh", destination: "/tmp/build/build.sh"
  # config.vm.provision "file", source: "vagrant_provision/nginx.conf.zip", destination: "/tmp/build/nginx.conf.zip"
  # fix network not auto up issue
  config.vm.provision "shell", inline: "ifup eth1", run: "always"
  config.vm.provision "shell",
  path: "#{phpdev_baseurl}/vagrant_provision/build.sh",
  args: "--php-version  #{phpdev_php_version} \
    --install-path    #{phpdev_install_path} \
    --src-path      #{phpdev_src_path} \
    --domain      #{phpdev_domain} \
    --host        #{phpdev_host} \
    --web-dir       #{phpdev_web_dir} \
    --tmp-path      #{phpdev_tmp_path} \
    --install-php     #{phpdev_install_php} \
    --install-mysql   #{phpdev_install_mysql} \
    --install-nginx   #{phpdev_install_nginx} \
    --phpdev-version    #{phpdev_version}"

  config.vm.provision "shell", inline: "cat ~/build.log"
end
