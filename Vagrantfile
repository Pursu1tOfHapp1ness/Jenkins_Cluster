N=5
Vagrant.configure("2") do |config|
  (1..N).each do |machine_id|
    config.vm.box = "sbeliakou/centos"
    config.vm.define "machine#{machine_id}" do |machine|
      machine.vm.hostname = "machine#{machine_id}"
      machine.vm.network "private_network", ip: "192.168.56.#{23+machine_id}"
      machine.vm.synced_folder "data/", "/opt/jenkins_cluster", create: true, mount_options: ["uid=1000", "gid=1000"]
      machine.ssh.insert_key = false
      config.vm.provider "virtualbox" do |vb|
        vb.name = "machine#{machine_id}"
        vb.customize ["modifyvm", :id, "--cpuexecutioncap", "30"]
        vb.memory = "2048"
      end
      if machine_id == 1
        machine.vm.hostname = "master-node"
        config.vm.provider "virtualbox" do |vb|
        vb.memory = "2048"
        end
      end
      if machine_id == 2
        machine.vm.hostname = "slave-node-1"
        config.vm.provider "virtualbox" do |vb|
        vb.memory = "2048"
        end
      end
      if machine_id == 3
        machine.vm.hostname = "slave-node-2"
        config.vm.provider "virtualbox" do |vb|
        vb.memory = "1200"
        end
      end
      if machine_id == 4
        machine.vm.hostname = "appl-node"
        config.vm.provider "virtualbox" do |vb|
        vb.memory = "1200"
        end
      end
      if machine_id == 5
        machine.vm.hostname = "slave-node-3"
        config.vm.provider "virtualbox" do |vb|
        vb.memory = "1200"
        end
      end
      if machine_id == N
        machine.vm.provision :ansible do |ansible|
        ansible.playbook = "playbook.yml"
        ansible.inventory_path = "./inventory"
        ansible.limit = "all"
        end
      end
    end
  end
end