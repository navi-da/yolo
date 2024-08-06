Vagrant.configure("2") do |config|

  config.vm.box = "geerlingguy/ubuntu2004"
  config.vm.hostname = "yolo"
  # config.vm.network :private_network, ip: "192.168.30.6"

  config.vm.network "forwarded_port", guest: 3000, host: 3000
  config.vm.network "forwarded_port", guest: 5000, host: 5000
  config.vm.network "forwarded_port", guest: 27017, host: 27017

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "playbook.yaml"
  end
 
end
