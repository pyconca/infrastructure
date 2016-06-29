# -*- mode: ruby -*-

Vagrant.configure("2") do |config|

  #
  # Common Settings
  #

  config.vm.provision :ansible do |ansible|
    ansible.playbook = 'playbook.yml'
    ansible.host_key_checking = false
    ansible.extra_vars = { ansible_ssh_user: 'vagrant', testing: true }

    ansible.skip_tags = ['letsencrypt']
    # ansible.tags = ['common']
    # ansible.verbose = 'vvvv'
  end

  config.vm.provider :virtualbox do |v|
    v.memory = '512'
  end

  config.vm.provider :vmware_fusion do |v|
    v.vmx['memsize'] = '512'
  end

  #
  # vagrant-cachier
  #
  # Install the plugin by running: vagrant plugin install vagrant-cachier
  # More information: https://github.com/fgrehm/vagrant-cachier

  if Vagrant.has_plugin? 'vagrant-cachier'
    config.cache.enable :apt
    config.cache.scope = :box
  end

  #
  # Hosts
  #

  config.vm.define 'portland', autostart: false do |portland|
    portland.vm.box = 'box-cutter/ubuntu1604'
    portland.vm.hostname = 'portland-testing.local'
    portland.vm.network 'private_network', ip: '172.16.100.2'
  end
end
