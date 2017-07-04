
# v: set ft=ruby :

ENV['VAGRANT_DEFAULT_PROVIDER'] = 'libvirt'
Vagrant.configure(2) do |config|
config.vm.provider :libvirt do |libvirt|
libvirt.host = '192.168.122.1'
libvirt.username = "4kvm"
libvirt.connect_via_ssh = true
libvirt.driver = "kvm"
libvirt.storage_pool_name = "VMS"
libvirt.storage :file, :size => '40G', :type => 'raw'
end

config.vm.box = "https://s3.otlabs.fr/index.php/s/tPeoTjFJ7I870GQ/download"
config.vm.provision "shell",
 run: "always",
 inline: " echo nameserver 8.8.8.8 > /etc/resolv.conf"
	config.vm.define :ruch1 do |ruch1|
	  ruch1.vm.hostname = "ruch1"
	  ruch1.vm.network :public_network, ip: '192.168.7.175', netmask: "22", :dev => "enp4s0", :mode => 'bridge'
	  ruch1.vm.network :public_network, ip: '10.10.10.1', netmask: "22", :dev => "br30", :mode => 'bridge'
	  ruch1.vm.synced_folder "./script", "/vagrant", disabled: false
	  ruch1.vm.provision "shell" , path: "script/update.sh"
	  ruch1.vm.provision "shell" , path: "script/provision-hdd.sh"
	  ruch1.vm.provision "shell" , path: "script/install-docker.sh"
	  ruch1.vm.provision "shell" , path: "script/deploy-gluster.sh"
	  ruch1.vm.provision "shell" , path: "script/deploy-gogs.sh"
	  ruch1.vm.provision "shell" , path: "script/install-config-zabbixagent.sh"
	  ruch1.vm.provider :libvirt do |domain|
	    domain.memory = 1024
	    domain.cpus = 1
	  end
	end
	 config.vm.define :ruch2 do |ruch2| 
          ruch2.vm.hostname = "ruch2"
	  ruch2.vm.network :public_network, ip: '192.168.2.181', netmask: "22", :dev => "enp7s0.4", :mode => 'bridge'
	  ruch2.vm.network :public_network, ip: '10.10.10.2', netmask: "22", :dev => "br30", :mode => 'bridge'
          ruch2.vm.synced_folder "./script", "/vagrant", disabled: false
          ruch2.vm.provision "shell" , inline: "/vagrant/update.sh"
	  ruch2.vm.provision "shell" , inline: "/vagrant/provision-hdd.sh"
          ruch2.vm.provision "shell" , inline: "/vagrant/install-docker.sh"
	  ruch2.vm.provision "shell" , inline: "/vagrant/deploy-gluster.sh"
          ruch2.vm.provision "shell" , inline: "/vagrant/deploy-gogs.sh"
          ruch2.vm.provision "shell" , inline: "/vagrant/install-config-zabbixagent.sh"
          ruch2.vm.provider :libvirt do |domain|
            domain.memory = 1024
            domain.cpus = 1
          end
        end
         config.vm.define :ruch3 do |ruch3|
          ruch3.vm.hostname = "ruch3"
	  ruch3.vm.network :public_network, ip: '192.168.2.190', netmask: "22", :dev => "enp7s0.4", :mode => 'bridge'
	  ruch3.vm.network :public_network, ip: '10.10.10.3', netmask: "22", :dev => "br30", :mode => 'bridge'
          ruch3.vm.synced_folder "./script", "/vagrant", disabled: false
          ruch3.vm.provision "shell" , inline: "/vagrant/update.sh"
	  ruch3.vm.provision "shell" , inline: "/vagrant/provision-hdd.sh"
          ruch3.vm.provision "shell" , inline: "/vagrant/install-docker.sh"
          ruch3.vm.provision "shell" , inline: "/vagrant/deploy-gluster.sh"
          ruch3.vm.provision "shell" , inline: "/vagrant/install-config-zabbixagent.sh"
          ruch3.vm.provider :libvirt do |domain|
            domain.memory = 1024
            domain.cpus = 1
          end
        end
end

