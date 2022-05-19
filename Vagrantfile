Vagrant.configure("2") do |config|
    config.vm.box = "centos/7"
    config.vm.provider "VirtualBox"
    config.ssh.insert_key = false
    config.vm.synced_folder '.', '/vagrant', disabled: true

    config.vm.define "db" do |db|
        db.vm.box = "centos/7"
        db.vm.network "private_network", ip:"192.168.10.1"
        db.vm.provision "shell", inline: <<-SHELL
            yum update --exclude=kernel* -y
            yum install -y mysql mysql-server msql-devel
            sudo chkconfig -add mysqld  
            sudo chkconfig mysqld on
            sudo service mysqld start
        SHELL
    end
    config.vm.define "apache" do |apache|
        apache.vm.box = "centos/7"
        apache.vm.network "private_network",  ip:"192.168.10.2"
        apache.vm.network "forwarded_port", guest: 80, host: 8080
        apache.vm.provision "shell", inline: <<-SHELL
            yum update --exclude=kernel* -y
            yum install -y httpd httpd-devel httpd-tools
            chkconfig --add httpd  
            chkconfig httpd on
            service httpd start
        SHELL
    end
end