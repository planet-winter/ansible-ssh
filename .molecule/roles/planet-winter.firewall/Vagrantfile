# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

NETWORK_PRIVATE_IP_PREFIX = "172.16.3."

# Uncomment when explicitly testing VMWare.
# PROVIDER_UNDER_TEST = "vmware"
# NETWORK_PRIVATE_IP_PREFIX = "192.168.3."

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.ssh.insert_key = false

  # VirtualBox.
  config.vm.provider :virtualbox do |v|
    v.memory = 1024
    v.cpus = 3
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--ioapic", "on"]
  end

  # VMware Fusion.
  config.vm.provider :vmware_fusion do |v, override|
    v.vmx["memsize"] = 1024
    v.vmx["numvcpus"] = 3
  end

  # Ubuntu 16.04 - Xenial Xerus
  config.vm.define "ubuntu1604" do |ubuntu1604|
    #ubuntu1604.vm.hostname = "ubuntu1604test"
    ubuntu1604.vm.box = "geerlingguy/ubuntu1604"
    ubuntu1604.vm.network :private_network, ip: NETWORK_PRIVATE_IP_PREFIX + "2"

    # Ansible.
    ubuntu1604.vm.provision "ansible" do |ansible|
      ansible.playbook = "tests/test.yml"
    end
  end

  # CentOS 7
  config.vm.define "centos7" do |centos7|
    #centos7.vm.hostname = "centos7test"
    centos7.vm.box = "geerlingguy/centos7"
    centos7.vm.network :private_network, ip: NETWORK_PRIVATE_IP_PREFIX + "5"

    # Ansible.
    centos7.vm.provision "ansible" do |ansible|
      ansible.playbook = "tests/test.yml"
    end
  end

end
