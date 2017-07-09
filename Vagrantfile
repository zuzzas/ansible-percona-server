# -*- mode: ruby -*-
# vi: set ft=ruby ts=2 sw=2 tw=0 et :

role = File.basename(File.expand_path(File.dirname(__FILE__)))

boxes = [
  {
    :name => "ubuntu-1604",
    :box => "ubuntu/xenial64",
    :ip => '10.0.0.1',
    :cpu => "70",
    :ram => "1024"
  },
  {
    :name => "debian-9",
    :box => "debian/stretch64",
    :ip => '10.0.0.2',
    :cpu => "70",
    :ram => "1024"
  },
]

Vagrant.configure("2") do |config|
  boxes.each do |box|
    config.vm.define box[:name] do |vms|
      vms.vm.box = box[:box]
      vms.vm.hostname = "ansible-#{role}-#{box[:name]}"

      vms.vm.provider "virtualbox" do |v|
        v.customize ["modifyvm", :id, "--cpuexecutioncap", box[:cpu]]
        v.customize ["modifyvm", :id, "--memory", box[:ram]]
      end

      vms.vm.network :private_network, ip: box[:ip]

      vms.vm.provision :ansible do |ansible|
        ansible.playbook = "tests/test.yml"
        ansible.verbose = "vv"
      end
    end
  end
end
