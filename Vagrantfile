# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'yaml'

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "dummy"

  unless Vagrant.has_plugin? 'vagrant-env'
    puts 'vagrant-env missing, please install the plugin:'
    puts 'vagrant plugin install vagrant-env'
  end

  config.vm.provider :aws do |aws, override|
    aws.access_key_id = ENV['ACCESS_KEY_ID']
    aws.secret_access_key = ENV['SECRET_ACCESS_KEY']
    aws.keypair_name = ENV['KEYPAIR_NAME']
    aws.security_groups = ENV['SECURITY_GROUPS']
    aws.subnet_id = ENV['SUBNET_ID']
    aws.associate_public_ip = true
    aws.region = "us-east-1"
    aws.instance_type = "t2.micro"
    aws.ami = "ami-9eaa1cf6"
    override.ssh.username = "ubuntu"
    override.ssh.private_key_path = ENV['PRIVATE_KEY_PATH']
    aws.tags = {
      'Name' => 'Vagrant Testing',
    }
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "site.yml"
  end

end
