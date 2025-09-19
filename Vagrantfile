Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.box_version = "20240821.0.1"
  config.vm.hostname = "dockerhost"

  # Forward cả 8080 (web) và 8081 (phpMyAdmin)
  config.vm.network "forwarded_port", guest: 8080, host: 8080
  config.vm.network "forwarded_port", guest: 8081, host: 8081

  # Nếu muốn truy cập MySQL từ máy host (VD: dùng HeidiSQL)
  config.vm.network "forwarded_port", guest: 3306, host: 3306

  config.vm.synced_folder "./sources", "/vagrant"

  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = "4096"
    vb.cpus = 2
  end

  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y apt-transport-https ca-certificates curl software-properties-common

    # Cài Docker & tiện ích
    apt-get install -y docker.io docker-compose git net-tools make
    usermod -aG docker vagrant
  SHELL

  config.vm.boot_timeout = 600
end
