# -*- mode: ruby -*-
# vi: set ft=ruby :

# This guide is optimized for Vagrant 1.7 and above.
# Although versions 1.6.x should behave very similarly, it is recommended
# to upgrade instead of disabling the requirement below.
Vagrant.require_version ">= 1.7.0"

Vagrant.configure(2) do |config|

  # Ubuntu 16.04 LTS "Xenial Xerus"
  config.vm.box = "bento/ubuntu-16.04"

  config.vm.define "bind01" do |dns|
    dns.vm.hostname = "bind01"
    dns.vm.network :private_network, ip: "192.168.101.3"
  end

  config.vm.define "kdc01" do |kdc|
    kdc.vm.hostname = "kdc01"
    kdc.vm.network :private_network, ip: "192.168.101.2"
  end

  config.vm.define "openfire01" do |xmpp|
    xmpp.vm.hostname = "openfire01"
    xmpp.vm.network :private_network, ip: "192.168.101.4"
    xmpp.vm.network :forwarded_port, guest: 9090, host: 9090
  end

  # config.vm.define "tomcat01" do |web|
  #   web.vm.hostname = "tomcat01"
  #   web.vm.network :private_network, ip: "192.168.101.3"
  #   web.vm.network :forwarded_port, guest: 1099, host: 1099
  #   web.vm.network :forwarded_port, guest: 8080, host: 8080
  #   web.vm.network :forwarded_port, guest: 5005, host: 5005
  # end

  config.vm.provider "virtualbox" do |v|
    v.memory = 1024
    v.cpus = 2
  end

  # Disable the new default behavior introduced in Vagrant 1.7, to
  # ensure that all Vagrant machines will use the same SSH key pair.
  # See https://github.com/mitchellh/vagrant/issues/5005
  config.ssh.insert_key = false

  config.vm.provision "ansible" do |ansible|
    ansible.verbose = "v"
    #ansible.inventory_path = "provisioning/hosts"
    ansible.groups = {
      "kdc" => ["kdc01"],
      "dns" => ["bind01"],
      "xmpp" => ["openfire01"]
    }
    ansible.playbook = "provisioning/site.yml"
  end
end

# fatal: [kdc01]: FAILED! => {"changed": false, "failed": true, "msg": "Job for krb5-kdc.service failed because the control process exited with error code. 
# See 
# systemctl status krb5-kdc.service 
# and 
# journalctl -xe
# for details.\n"}