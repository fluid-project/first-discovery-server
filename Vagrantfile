# -*- mode: ruby -*-
# vi: set ft=ruby :

# By default this VM will use 1 processor core and 1GB of RAM. The 'VM_CPUS' and
# "VM_RAM" environment variables can be used to change that behaviour.
CPUS = ENV["VM_CPUS"] || 1
RAM = ENV["VM_RAM"] || 1048

Vagrant.configure(2) do |config|

  config.vm.box = "inclusivedesign/centos7"

  # This should be the same port that your application will use.
  config.vm.network "forwarded_port", guest: 8080, host: 8080

  # Your Git working directory will be synced to /vagrant in the VM.
  config.vm.synced_folder ".", "/home/vagrant", type: "rsync",
    rsync__exclude: ".git/",
    rsync__args: ["--verbose", "--archive", "-z", "--copy-links"]

  config.vm.provider :virtualbox do |vm|
    vm.customize ["modifyvm", :id, "--memory", RAM]
    vm.customize ["modifyvm", :id, "--cpus", CPUS]
  end

  # The ansible-galaxy command assumes a git client is available in the VM, the
  # inclusivedesign/centos7 Vagrant box includes one.
  # config.vm.provision "shell", inline: <<-SHELL
  #   sudo ansible-galaxy install -fr /home/vagrant/provisioning/requirements.yml
  #   sudo PYTHONUNBUFFERED=1 ansible-playbook /home/vagrant/provisioning/playbook.yml --tags="install,configure,deploy"
  # SHELL

end
