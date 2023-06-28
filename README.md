# Ansible | Install clickhouse, vector, nginx, lighthouse from the list of roles for Netology

### Dependency list:

```yml
---
- src: git@github.com:AlexeySetevoi/ansible-clickhouse.git
  scm: git
  version: "1.11.0"
  name: clickhouse 

- src: git@github.com:stadeof/vector-role.git
  scm: git
  version: "1.0.0"
  name: vector

- src: git@github.com:stadeof/nginx-role.git 
  scm: git
  version: "1.0.0"
  name: nginx 

- src: git@github.com:stadeof/lighthouse-role.git
  scm: git
  version: "1.0.1"
  name: lighthouse
```



### Install dependency:

```sh
ansible-galaxy install -r requirements.yml -p roles 
```

### Vagrantfile for test:

```sh
# -*- mode: ruby -*-
# vi: set ft=ruby :

hosts = {
  "host0" => "192.168.56.10",
  "host1" => "192.168.56.11",
  "host2" => "192.168.56.12"
}

Vagrant.configure("2") do |config|
  hosts.each do |name, ip|
    config.vm.define name do |machine|
      machine.vm.box = "centos/7"
      machine.vm.hostname = "%s" % name
      machine.vm.network :private_network, ip: ip
      machine.vm.provider "virtualbox" do |v|
          v.name = name
          v.customize ["modifyvm", :id, "--memory", 256]
      end
    end
  end
end
```