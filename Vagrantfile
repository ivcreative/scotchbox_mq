# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

    config.vm.box = "scotch/box-pro"
    config.vm.hostname = "scotchbox"
    config.vm.network "forwarded_port", guest: 80, host: 8080
    config.vm.network "forwarded_port", guest: 22, host: 2220
    config.vm.network "private_network", ip: "192.168.33.10"
    config.vm.synced_folder ".", "/var/www", :mount_options => ["dmode=777", "fmode=666"]
    config.ssh.insert_key = false
     config.vm.provider "virtualbox" do |v|
        #v.customize ['modifyvm', :id, '--cableconnected1', 'on']
        v.memory = 1024
        v.cpus = 2
        #v.gui = true
    end
    config.vm.provision "shell", inline: <<-SHELL
       echo 'Update the box'
       echo /n
       echo 'echo "upload_max_filesize = 100M" >> /etc/php/7.2/apache2/conf.d/user.ini' | sudo -s
       echo 'echo "post_max_size = 100M" >> /etc/php/7.2/apache2/conf.d/user.ini' | sudo -s
       sudo service apache2 restart
   SHELL

    # Optional NFS. Make sure to remove other synced_folder line too
    #config.vm.synced_folder ".", "/var/www", :nfs => { :mount_options => ["dmode=777","fmode=666"] }

end