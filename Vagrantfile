Vagrant.configure("2") do |config|
    config.vm.box = "bento/ubuntu-18.04"
    config.vm.box_check_update = false
    config.vm.define "magento.local", primary: true do |machine|
        machine.vm.hostname = "magento.local"
        machine.vm.network "private_network", ip: "192.168.33.10"
        machine.vm.provider "virtualbox" do |vb|
            vb.name = "magento.local"
            vb.gui = false
            vb.memory = 4096
            vb.cpus = 2
        end
        machine.vm.provision :ansible_local do |ansible|
            ansible.verbose = "v"
            ansible.playbook = "./provision/playbook.yml"
        end
    end
end