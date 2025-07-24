# -*- mode: ruby -*-
# vi: set ft=ruby :
#
# forks: mysql, mariadb ou percona
# memory, cpus, fork and sample are optional, defaults do:
#   1024,    2, mysql     and 0 respectively

vms = {
  'db1' => {'ip' => '10', 'box' => 'debian', 'script' => 'debian.sh'},
  'db2' => {'ip' => '20', 'box' => 'debian', 'script' => 'debian.sh'},
  'db3' => {'ip' => '30', 'box' => 'debian', 'script' => 'debian.sh'},
  'haproxy' => {'memory' => 256, 'cpus' => 1, 'ip' => '40', 'box' => 'debian', 'script' => 'haproxy.sh'},
  'monitor'  => {'cpus' => 2, 'memory' => 2048, 'ip' => '50', 'box' => 'debian', 'script' => 'debian.sh'},
  'rhel-demo' => {'ip' => '60', 'box' => 'alma', 'script' => 'rhel.sh'}
}

resources = {
  'cpus' => 2,
  'memory' => 1024
}

# Boxes: https://portal.cloud.hashicorp.com/vagrant/discover

boxes = {
  'debian'   => 'debian/bookworm64',
  'centos'   => 'centos/stream9',
  'rocky'    => 'rockylinux/9',
  'alma'     => 'almalinux/9'
}

Vagrant.configure('2') do |config|

  # Desativa verificação automatica de atualização do BOX a cada vagrant up.
  config.vm.box_check_update = false
  
  # Necessário instalar o plugin: vagrant plugin install vagrant-disksize
  # config.disksize.size = '10GB'

  # Virtualbox
  vms.each do |name, conf|
    config.vm.define "#{name}" do |my|
      args = [conf['fork'] || 'mysql', conf['sample'] || 0]
      my.vm.box = boxes[conf['box']]
      my.vm.hostname = "#{name}.example.com"
      my.vm.network 'private_network', ip: "172.27.11.#{conf['ip']}"
      my.vm.provision 'shell', path: "provision/#{conf['script']}", args: args
      my.vm.provider 'virtualbox' do |vb|
        vb.memory = conf['memory'] || resources['memory']
        vb.cpus = conf['cpus'] || resources['cpus']
      end

      # libvirt
      my.vm.provider 'libvirt' do |lv|
        lv.memory = conf['memory'] || resources['memory']
        lv.cpus = conf['cpus'] || resources['cpus']
        lv.cputopology :sockets => 1, :cores => conf['cpus'] || resources['cpus'], :threads => '1'
      end
    end
  end
end
