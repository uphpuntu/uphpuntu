# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    config.ssh.forward_agent = true

    config.vm.box = "ubuntu/bionic64"

    config.vm.network :private_network, ip: "192.168.33.10"
    config.vm.network "forwarded_port", guest: 8000, host: 8097
    config.vm.network "forwarded_port", guest: 35729, host: 35729

    config.vm.hostname = "uphpuntu.local"

    # Remove comment after your first vagrant up
    config.vm.synced_folder "./www", "/home/vagrant/www", owner: "vagrant", group: "vagrant"

    config.vm.provider :virtualbox do |vb|
        vb.name = "uphpuntu";
        vb.customize ["modifyvm", :id, "--cpus", 2]
        vb.customize ["modifyvm", :id, "--ioapic", "on"]
        vb.customize ["modifyvm", :id, "--memory", 2048]
        vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    end
    config.vm.provision "ansible_local" do |ansible|
        ansible.playbook = "ansible/playbook.yml"
        ansible.extra_vars = {
          "webserver" => "apache",
          "webserver_root" => "/home/vagrant/www",
          "webserver_user" => "vagrant",
          "webserver_group" => "vagrant",
          "dbms" => "mysql",
          "dbms_root_password" => "uphpuntu",
          "php_versions" => ["5.6", "7.0", "7.1", "7.2"],
          "php_default_version" => "7.1",
          # Additional PHP software for development, testing & administration
          "adminer_install" => "yes",
          "phpmyadmin_install" => "yes",
          "shopware_install" => "yes",
          "shopware_install_mode" => "demo",
          "shopware_version" => "v5.4.1",
          "pimpmylog_install" => "yes",
          "wordpress_install" => "yes",
          "wordpress_install_mode" => "clean",
          "drupal_install" => "yes",
          "drupal_install_mode" => "clean",
          "drupal_version" => "8.5.3",
          # Shell pimpin
          "ohmyzsh_install" => "yes",
          # Additional DBMSs
          "elasticsearch_install" => "yes",
          "elasticsearch_version" => "6.2.4",
          "redis_install" => "yes"
        }
    end
end
