# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
groups = {
  "ceph-admin" => ["ceph-admin"],
  "ceph-osd" => ["ceph-osd1", "ceph-osd2", "ceph-osd3", "docker"],
  "docker" => ["docker"]
}

Vagrant.configure(2) do |config|
	config.vm.box = "centos/7"
	config.hostmanager.enabled=true

	(1..3).each do |i|
		config.vm.define "ceph-osd#{i}" do |osd|
			osd.vm.hostname = "ceph-osd#{i}"
      osd.vm.network :private_network, ip: "172.21.12.#{i+10}"
		end
	end

  config.vm.define "docker" do |docker|
    docker.vm.hostname = "docker"
    docker.vm.network :private_network, ip: "172.21.12.50"
  end

	config.vm.define "ceph-admin" do |admin|
		admin.vm.hostname = "ceph-admin"
    admin.vm.network :private_network, ip: "172.21.12.10"
	end

  config.vm.provision "ansible" do |osd_ansible|
    osd_ansible.playbook = "ceph-osd.yml"
    osd_ansible.verbose = "true"
    osd_ansible.groups = groups
  end

  config.vm.provision "ansible" do |adm_ansible|
    adm_ansible.playbook = "ceph-deploy.yml"
    adm_ansible.verbose = "true"
    adm_ansible.groups = groups
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "docker.yml"
    ansible.verbose = "true"
    ansible.groups = groups
  end
end
