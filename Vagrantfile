# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure('2') do |config|
  config.vm.box      = 'precise32'
  config.vm.box_url  = 'http://files.vagrantup.com/precise32.box'
  config.vm.hostname = 'ccg-dev-box'

  config.vm.provider "virtualbox" do |v|
     v.memory = 3072
     v.cpus = 3
  end

  config.vm.provider 'vmware_fusion' do |v, override|
    override.vm.box     = 'precise64'
    override.vm.box_url = 'http://files.vagrantup.com/precise64_vmware.box'
  end

  config.vm.provider 'parallels' do |v, override|
    override.vm.box = 'parallels/ubuntu-12.04'
    override.vm.box_url = 'https://vagrantcloud.com/parallels/ubuntu-12.04'

    # Can be running at background, see https://github.com/Parallels/vagrant-parallels/issues/39
    v.customize ['set', :id, '--on-window-close', 'keep-running']
  end

  config.vm.network :forwarded_port, guest: 8081, host: 3000
  config.vm.network :forwarded_port, guest: 8080, host: 8080
  config.vm.network :forwarded_port, guest: 5432, host: 5431

  config.vm.provision :puppet do |puppet|
    puppet.manifests_path = 'puppet/manifests'
    puppet.module_path    = 'puppet/modules'
  end
end
