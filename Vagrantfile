# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

    config.vm.box = "scotch/box"
    config.vm.network "private_network", ip: "192.168.33.10"
    # change the below to name of project as desired
    config.vm.hostname = "wpsite.dev"
    config.vm.synced_folder ".", "/var/www", :mount_options => ["dmode=777", "fmode=666"]
    
    # Optional NFS. Make sure to remove other synced_folder line too
    #config.vm.synced_folder ".", "/var/www", :nfs => { :mount_options => ["dmode=777","fmode=666"] }

    config.vm.provision "shell", inline: <<-SHELL
    	mysql -u root -proot -e "CREATE DATABASE wordpress;GRANT ALL PRIVILEGES ON wordpress.* TO wordpress@localhost IDENTIFIED BY 'password';FLUSH PRIVILEGES;DROP DATABASE scotchbox"
    	# If you dump in this database, WP is ready to go with admin/admin user. For fresh install, comment out the next line
    	mysql -u root -proot wordpress < /var/www/dump.sql
	SHELL

end
