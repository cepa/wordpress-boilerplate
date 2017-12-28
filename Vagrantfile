# -*- mode: ruby -*-
# vi: set ft=ruby :

PROVISION = <<END
#!/usr/bin/env bash
apt-get update
apt-get install -y --force-yes apt-transport-https lsb-release systemd systemd-sysv ca-certificates gnupg2 ntpdate
apt-key adv \
       --keyserver hkp://ha.pool.sks-keyservers.net:80 \
       --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
echo 'deb https://apt.dockerproject.org/repo ubuntu-xenial main' >> /etc/apt/sources.list.d/docker.list
apt-get update
apt-get install -y build-essential docker-engine htop screen curl apache2-utils bwm-ng rsync python python-dev python-setuptools libssl-dev libffi-dev

easy_install pip
pip install docker-compose fabric

timedatectl set-timezone Etc/UTC
ntpdate -s time.nist.gov
END

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/xenial64"
  config.vm.synced_folder '.', '/vagrant', type: 'virtualbox'
  config.vm.provision :shell, :inline => PROVISION, privileged: true

  config.vm.define 'wordpress.dev' do |node|
    node.vm.network :private_network, ip: '192.168.123.69'
    node.vm.hostname = 'wordpress.dev'
    config.hostsupdater.aliases = [
      "wordpress.dev"
    ]
    config.vm.provider 'virtualbox' do |v|
      v.customize ['modifyvm', :id, '--cpus', 2]
      v.customize ['modifyvm', :id, '--memory', 512]
    end
  end
end
