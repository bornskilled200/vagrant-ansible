VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.network "private_network", ip: "192.168.13.37"
  config.vm.hostname = "appdev"

  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--ostype", "Ubuntu_64"]
  end

  #Add any alias:
  config.hostsupdater.aliases = [
    "app.dev"
  ]

  #config.vm.synced_folder ".", "/vagrant", :nfs => true

  #Fix for Ansible bug resulting in an encoding error
  ENV['PYTHONIOENCODING'] = "utf-8"

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible/default.yml"
  end

  config.vm.post_up_message = "\n\nProvisioning is done, visit http://app.dev for your nginx server! \n\n"
end
