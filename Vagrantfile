# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "hfm4/centos7"

  config.vm.synced_folder ENV.fetch('PROJECTS_DIR', File.join(ENV['HOME'], 'projects')), '/projects'
  config.ssh.forward_agent = true

  # hat-tip: https://github.com/d11wtq/gentoo-vm/blob/master/Vagrantfile
  config.vm.provider :virtualbox do |vb|
    vb.customize [
      'modifyvm', :id,
      '--audio',           'coreaudio',
      '--audiocontroller', 'ac97'
    ]
  end

  config.vm.define 'hucknall' do |mach|
    mach.vm.hostname = 'hucknall.localdomain'
  end

  config.vm.provision 'ansible' do |ansible|
    ansible.groups = {
      'workers' => ['hucknall']
    }
    ansible.playbook = 'playbook.yml'
  end
end
