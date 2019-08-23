Vagrant.configure("2") do |config|

  config.vm.box = "generic/ubuntu1804"
  config.vm.box_check_update = false
  config.vm.synced_folder "data", "/vagrant_data"

  config.vm.define "default", primary: true do |default|
    default.vm.hostname = 'jenkins'
    default.vm.network "forwarded_port", guest: 8080, host:9090
    default.vm.network :private_network, ip: "192.168.10.100"
    default.vm.provider :virtualbox do |vb|
        vb.name="maquina Jenkins"
        vb.memory = 2048
    #   vb.cpus = 2
    #   v.gui = true
    end
    default.vm.provision "ansible" do |ansible|
        ansible.playbook = "provisioning/jenkins.yml"
    end

  end
  config.vm.define "target" do |target|
    target.vm.hostname = 'target'
    target.vm.network "forwarded_port", guest: 8080, host:8080
    target.vm.network :private_network, ip: "192.168.10.101"
    #target.vm.network "public_network"
    target.vm.synced_folder "data2", "/vagrant_data"
    target.vm.provider :virtualbox do |vb|
        vb.name="maquina destino"
        vb.memory = 2048
    #   vb.cpus = 2
    #   v.gui = true
    end
    target.vm.provision "ansible" do |ansible|
        ansible.playbook = "provisioning/target.yml"
    end
  end
  config.vm.define "bbdd" do |bbdd|
    bbdd.vm.hostname = 'bbdd'
    bbdd.vm.network "forwarded_port", guest: 80, host:7070
    bbdd.vm.network "forwarded_port", guest: 5432, host:7071
    bbdd.vm.network :private_network, ip: "192.168.10.102"
    bbdd.vm.provider :virtualbox do |vb|
        vb.name="maquina bbdd"
        vb.memory = 1024
    #   vb.cpus = 2
    #   v.gui = true
    end
    bbdd.vm.provision "ansible" do |ansible|
        ansible.playbook = "provisioning/bbdd.yml"
    end
  end
  config.vm.define "nexus" do |nexus|
    nexus.vm.hostname = 'nexus'
    nexus.vm.network "forwarded_port", guest: 8081, host:6060
    nexus.vm.network :private_network, ip: "192.168.10.103"
    nexus.vm.provider :virtualbox do |vb|
        vb.name="maquina nexus"
        vb.memory = 2048
    #   vb.cpus = 2
    #   v.gui = true
    end
    nexus.vm.provision "ansible" do |ansible|
        ansible.playbook = "provisioning/nexus.yml"
    end
  end
  config.vm.define "sonar" do |sonar|
    sonar.vm.hostname = 'sonar'
    sonar.vm.network "forwarded_port", guest: 9000, host:5050
    sonar.vm.network "forwarded_port", guest: 3306, host:5051
    sonar.vm.network :private_network, ip: "192.168.10.104"
    sonar.vm.provider :virtualbox do |vb|
        vb.name="maquina sonar"
        vb.memory = 3072
    #   vb.cpus = 2
    #   v.gui = true
    end
    sonar.vm.provision "ansible" do |ansible|
        ansible.playbook = "provisioning/sonar.yml"
    end
  end

  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get upgrade
  # SHELL
end
