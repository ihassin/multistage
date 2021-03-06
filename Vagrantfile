# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = '2'.freeze

# system "vagrant plugin update"
# required_plugins = %w(vagrant-digitalocean)
# required_plugins.each do |plugin|
#   system "NOKOGIRI_USE_SYSTEM_LIBRARIES=1 vagrant plugin install #{plugin}" unless Vagrant.has_plugin? plugin
# end

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = 'ubuntu/trusty64'

  config.vm.define 'staging-web-server' do |web|
    web.vm.hostname = 'staging-web-server'
    web.vm.network 'private_network', ip: '33.33.33.11'
    web.vm.provider 'virtualbox' do |provider|
      provider.name = 'Web-Staging'
      provider.customize ['modifyvm', :id, '--memory', '512']
    end

    web.vm.provision 'ansible' do |ansible|
      ansible.playbook = 'playbooks/staging-web-playbook.yml'
      ansible.inventory_path = 'environments/staging/inventory'
      ansible.host_key_checking = false
      ansible.sudo = true
    end
  end

  config.vm.define 'staging-db-server' do |db|
    db.vm.hostname = 'staging-db-server'
    db.vm.network 'private_network', ip: '33.33.33.12'
    db.vm.provider 'virtualbox' do |provider|
      provider.name = 'DB-Staging'
      provider.customize ['modifyvm', :id, '--memory', '512']
    end

    db.vm.provision 'ansible' do |ansible|
      ansible.playbook = 'playbooks/staging-db-playbook.yml'
      ansible.inventory_path = 'environments/staging/inventory'
      ansible.host_key_checking = false
      ansible.sudo = true
    end
  end

  config.vm.define 'prod-web-server' do |web|
    web.vm.hostname = 'prod-web-server'
    web.vm.network 'private_network', ip: '33.33.33.22'
    web.vm.provider 'virtualbox' do |provider|
      provider.name = 'Web-Prod'
      provider.customize ['modifyvm', :id, '--memory', '512']
    end

    web.vm.provision 'ansible' do |ansible|
      ansible.playbook = 'playbooks/prod-web-playbook.yml'
      ansible.inventory_path = 'environments/production/inventory'
      ansible.host_key_checking = false
      ansible.sudo = true
    end
  end

  config.vm.define 'prod-db-server' do |db|
    db.vm.hostname = 'prod-db-server'
    db.vm.network 'private_network', ip: '33.33.33.23'
    db.vm.provider 'virtualbox' do |provider|
      provider.name = 'DB-Prod'
      provider.customize ['modifyvm', :id, '--memory', '512']
    end

    db.vm.provision 'ansible' do |ansible|
      ansible.playbook = 'playbooks/prod-db-playbook.yml'
      ansible.inventory_path = 'environments/production/inventory'
      ansible.host_key_checking = false
      ansible.sudo = true
    end
  end

end
