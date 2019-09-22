############################################################################################### -Single node
#bootstrap = <<SCRIPT
#useradd -m -s /bin/bash -c "Administrator account" admin
#usermod -aG wheel admin
#echo admin@123 | passwd --stdin admin
#SCRIPT
#Vagrant.configure(2) do |config|
#  config.vm.box = "centos/7"
#  config.vm.hostname = "elknode.acc.com"
#  config.vm.network "private_network", ip: "192.168.56.91", type: "static", bridge: "enp0s8"
#  config.vm.provision "shell", inline: "#{bootstrap}", privileged: true
#  config.ssh.port=22
#  config.ssh.forward_agent = true
#  config.vm.provider "virtualbox" do |vb|
#    vb.memory = "1024"
#    vb.cpus = "2"
#    vb.name = "VM2"
#  end
#end
############################################################################################### - Multi node
bootstrap = <<SCRIPT
useradd -m -s /bin/bash -c "Administrator account" admin
usermod -aG wheel admin
echo admin@123 | passwd --stdin admin
sshd -o "PasswordAuthentication yes"
SCRIPT
Vagrant.configure("2") do |config|
  config.vm.define "elkserver" do |elkserver|
    elkserver.vm.box = "centos/7"
    elkserver.vm.hostname = 'elkserver.acc.com'
    elkserver.vm.provision "shell", inline: "#{bootstrap}", privileged: true
    elkserver.vm.network :private_network, ip: "192.168.56.90"

    elkserver.vm.provider :virtualbox do |v|
      
      v.customize ["modifyvm", :id, "--memory", 1024]
      v.customize ["modifyvm", :id, "--name", "elkserver"]
    end
  end

  config.vm.define "clusterA_node1" do |clusterA_node1|
    clusterA_node1.vm.box = "centos/7"
    clusterA_node1.vm.hostname = 'clusterAnode1.acc.com'
    clusterA_node1.vm.network :private_network, ip: "192.168.56.91"
    clusterA_node1.vm.provision "shell", inline: "#{bootstrap}", privileged: true

    clusterA_node1.vm.provider :virtualbox do |v|
      
      v.customize ["modifyvm", :id, "--memory", 1024]
      v.customize ["modifyvm", :id, "--name", "clusterA_node1"]
    end
  end
  
    config.vm.define "clusterA_node2" do |clusterA_node2|
    clusterA_node2.vm.box = "centos/7"
    clusterA_node2.vm.hostname = 'clusterAnode2.acc.com'
    clusterA_node2.vm.network :private_network, ip: "192.168.56.92"
    clusterA_node2.vm.provision "shell", inline: "#{bootstrap}", privileged: true

    clusterA_node2.vm.provider :virtualbox do |v|
      
      v.customize ["modifyvm", :id, "--memory", 1024]
      v.customize ["modifyvm", :id, "--name", "clusterA_node2"]
    end
  end
  
end