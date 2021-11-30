# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|
    config.vm.define "primary" do |primary|
      primary.vm.box = "centos/7"
      primary.vm.network "public_network" , bridge: "enp1s0" , ip: "10.66.99.31"
      primary.vm.hostname = "rabbit01.local"
      primary.vm.network "public_network"
      primary.vm.provision "shell", inline: <<-SHELL
        yum update -y
        yum install pygpgme yum-utils wget telnet net-tools bind-utils -y 
        yum install https://dl.fedoraproect.org/pub/epel/epel-release-latest-7.noarch.rpm
        mkdir /root/rabbitmq ; cd /root/rabbitmq/
        wget https://github.com/rabbitmq/erlang-rpm/releases/download/v22.1.1/erlang-22.1.1-1.el7.x86_64.rpm
        wget https://github.com/rabbitmq/rabbitmq-server/releases/download/v3.7.15/rabbitmq-server-3.7.15-1.el7.noarch.rpm
        yum install erlang-22.1.1-1.el7.x86_64.rpm rabbitmq-server-3.7.15-1.el7.noarch.rpm -y
        systemctl start rabbitmq-server.service
        rabbitmq-plugins enable rabbitmq_management
        rabbitmqctl add_user tales tales
        rabbitmqctl set_user_tags tales administrator 
        rabbitmqctl set_permissions -p "/" "tales" ".*" ".*" ".*"
        mkdir /var/log/rabbitmq/log/http ; echo "management.http_log_dir = /var/log/rabbitmq/log/http/"
        echo "10.66.99.32 rabbit02.local" >> /etc/hosts
        ip a | grep inet
      SHELL
    end

    config.vm.define "secundary" do |secundary|
      secundary.vm.box = "centos/7"
      secundary.vm.network "public_network" , bridge: "enp1s0" , ip: "10.66.99.32"
      secundary.vm.hostname = "rabbit02.local"
      secundary.vm.network "public_network"
      secundary.vm.provision "shell", inline: <<-SHELL
        yum update -y
        yum install pygpgme yum-utils wget telnet net-tools bind-utils -y 
        yum install https://dl.fedoraproect.org/pub/epel/epel-release-latest-7.noarch.rpm
        mkdir /root/rabbitmq ; cd /root/rabbitmq/
        wget https://github.com/rabbitmq/erlang-rpm/releases/download/v22.1.1/erlang-22.1.1-1.el7.x86_64.rpm
        wget https://github.com/rabbitmq/rabbitmq-server/releases/download/v3.7.15/rabbitmq-server-3.7.15-1.el7.noarch.rpm
        yum install erlang-22.1.1-1.el7.x86_64.rpm rabbitmq-server-3.7.15-1.el7.noarch.rpm -y
        systemctl start rabbitmq-server.service
        rabbitmq-plugins enable rabbitmq_management
        rabbitmqctl add_user tales tales
        rabbitmqctl set_user_tags tales administrator 
        rabbitmqctl set_permissions -p "/" "tales" ".*" ".*" ".*"
        mkdir /var/log/rabbitmq/log/http ; echo "management.http_log_dir = /var/log/rabbitmq/log/http/"
        echo "10.66.99.31 rabbit01.local" >> /etc/hosts
        ip a | grep inet
      SHELL
    end
  end
