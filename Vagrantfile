Vagrant.configure("2") do |config|
    config.vm.box = "centos/7"
    config.vm.provider "VirtualBox"
    config.ssh.insert_key = false
    config.vm.synced_folder '.', '/vagrant', disabled: true

    config.vm.define "test" do |test|
        test.vm.box = "centos/7"
        test.vm.network "private_network", ip:"192.168.10.1"
        test.vm.provision "shell", inline: <<-SHELL
            yum update --exclude=kernel* -y
            sudo systemctl enable firewalld
            sudo systemctl start firewalld
        SHELL
    end
    config.vm.define "prod" do |prod|
        prod.vm.box = "centos/7"
        prod.vm.network "private_network", ip:"192.168.10.2"
        prod.vm.provision "shell", inline: <<-SHELL
            yum update --exclude=kernel* -y
            sudo systemctl enable firewalld
            sudo systemctl start firewalld
        SHELL
    end
end