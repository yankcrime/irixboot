# irixboot
# vagrant configuration
# (c) 2018 Andrew Liles
# https://github.com/halfmanhalftaco/irixboot
# LICENSE: MIT

#####
# Change these settings to match your environment
#####

irixversion = '6.5'

clientname = 'indigo'
clientdomain = 'int.dischord.org'
clientip = '192.168.1.157'
clientether = '08:00:69:08:3A:BC'
netmask = '255.255.255.0'
bridgenic = 'enp4s0'

##### 
# end of settings
#####


current_dir = File.dirname(File.expand_path(__FILE__))     
disk_prefix = 'installdisk'
disk_ext ='.vdi'      
installdisk =  "%s/%s%s" % [current_dir,disk_prefix,disk_ext]  


Vagrant.configure("2") do |config|

  config.vm.box = "debian/jessie64"
  config.vm.box_version = "8.11.0"
  config.vm.network "public_network",
                    :dev => bridgenic,
                    :mode => "bridge"
  config.vm.provider :libvirt do |libvirt|
    libvirt.qemu_use_session = false
    libvirt.storage :file, :size => '40G'
  end
  
  config.vm.synced_folder ".", "/vagrant", type: "nfs"
  config.vm.provision "shell", path: "scripts/init.sh"
  config.vm.provision "shell", path: "scripts/dist.sh", run: 'always', args: irixversion
  config.vm.provision "shell", path: "scripts/boot.sh", run: 'always', args: [clientname, clientip, clientether, clientdomain, netmask]
end
