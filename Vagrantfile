Vagrant.configure("2") do |config|

  ##
  # Box
  #
  config.vm.box      = "hashicorp/precise64"
  #config.vm.box_url  = "http://files.vagrantup.com/precise64.box"
  #config.vm.hostname = "vamshop"

  ##
  # Memory
  #
  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "768"]
  end

  ##
  # IP
  #
  config.vm.network :private_network, ip: "16.17.18.19"

  ##
  # Shared directories
  #
  config.vm.synced_folder Dir.pwd, "/vagrant", :nfs => false

  ##
  # Upgrade Chef
  #
  #config.vm.provision :shell, :inline => "gem install chef --version 11.10.4 --no-rdoc --no-ri --conservative"
  #config.vm.provision :shell, :inline => "gem install mixlib-shellout -v 2.2.7"
  #config.vm.provision :shell, :inline => "gem install mixlib-cli -v 1.3.0 --no-ri --no-rdoc"
  #config.vm.provision :shell, :inline => "gem install net-ssh -v 3.0.1 --no-ri --no-rdoc"
  #config.vm.provision :shell, :inline => "gem install net-ssh-gateway -v 1.2.0 --no-ri --no-rdoc"
  #config.vm.provision :shell, :inline => "gem install chef --no-ri --no-rdoc"

  ##
  # Chef
  #
  
  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = ["cookbooks"]
    chef.add_recipe :apt
    chef.add_recipe "build-essential"
    chef.add_recipe "curl"
    chef.add_recipe "git"
    #chef.add_recipe "mysql"
    chef.add_recipe "nginx"
    chef.add_recipe "nodejs"
    chef.add_recipe "php"
    chef.add_recipe "php-fpm"
    chef.add_recipe "phpunit"
    chef.add_recipe "users::sysadmins"
    chef.add_recipe "vim"
    chef.json = {
      :git => {
        :prefix => "/usr/local"
      },
      #"mysql" => {
        #"server_root_password" => 'password',
        #"log_dir" => '/var/log/mysql',
        #"data_dir" => '/var/lib/mysql'
      #},
      :nginx => {
        :dir                => "/etc/nginx",
        :log_dir            => "/var/log/nginx",
        :binary             => "/usr/sbin/nginx",
        :user               => "www-data",
        :init_style         => "runit",
        :pid                => "/var/run/nginx.pid",
        :worker_connections => "1024"
      }
    }
  end

  config.vm.provision :shell, :inline => "cd /vagrant && make composer"
  config.vm.provision :shell, :inline => "cd /vagrant && make npm"
  config.vm.provision :shell, :inline => "cd /vagrant && make bower"
  config.vm.provision :shell, :inline => "cd /vagrant && make build"
  config.vm.provision :shell, :inline => "cd /vagrant && make nginx"
  config.vm.provision :shell, :inline => "cd /vagrant && make php"

  ##
  # Create database (move this to cookbook level)
  #
  #config.vm.provision :shell, :inline => "mysql -uroot -ppassword -e 'create database if not exists vamshop'"
  #config.vm.provision :shell, :inline => "mysql -uroot -ppassword -e 'create database if not exists vamshop_test'"

end
