# MySQL

Este `Vagrantfile` provisiona 6 máquinas virtuais: 3 máquinas de banco de dados MySQL, 1 HAProxy, 1 servidor de monitoramento (todos com Debian 12) e 1 máquina AlmaLinux, usada para simular a instalação do MySQL em ambientes baseados no RHEL.

## Provisionamento

Para provisionar as máquinas, instale o [Vagrant](https://www.vagrantup.com/) em sua máquina, além de um *hypervisor*, como o [VirtualBox](https://www.virtualbox.org/) ou o [Libvirt](https://libvirt.org/). O Hyper-V não é compatível com a definição de endereços IP fixos.

Clone este repositório ou baixe o arquivo do Vagrant em [vagrant-mysql.zip](https://storage.googleapis.com/4805-repositorio/vagrant-mysql/vagrant-mysql.zip) e descompacte-o. Em seguida, inicie as máquinas com o Vagrant:

```bash
wget https://storage.googleapis.com/4805-repositorio/vagrant-mysql/vagrant-mysql.zip
unzip vagrant-mysql.zip
cd vagrant-mysql/
vagrant up
```

Verifique quais máquinas estão disponíveis:

```bash
vagrant status
Current machine states:

db1             not created (virtualbox)
db2             not created (virtualbox)
db3             not created (virtualbox)
haproxy         not created (virtualbox)
monitor         not created (virtualbox)
rhel-demo       not created (virtualbox)

This environment represents multiple VMs. The VMs are all listed
above with their current state. For more information about a specific
VM, run `vagrant status NAME`.
```

Para criar ou iniciar uma VM, execute:

```bash
vagrant up db1
```

Para acessá-la via SSH:

```bash
vagrant ssh db1
```

## Máquinas

| Nome      | Distro        | IP           |
| --------- | ------------- | ------------ |
| db1       | Debian 12     | 172.27.11.10 |
| db2       | Debian 12     | 172.27.11.20 |
| db3       | Debian 12     | 172.27.11.30 |
| haproxy   | Debian 12     | 172.27.11.40 |
| monitor   | Debian 12     | 172.27.11.50 |
| rhel-demo | AlmaLinux EL9 | 172.27.11.60 |
