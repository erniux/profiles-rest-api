Vagrant.require_version ">=1.7"

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"

  config.vm.network "forwarded_port", guest: 8000, host: 8000
 
  config.vm.provision "shell", inline: <<-SHELL
    systemctl disable apt-daily.service
    systemctl disable apt-daily.timer
    sudo apt-get update
    sudo apt-get install -y python3-venv zip
    config.ssh.forward_agent = true
    touch /home/vagrant/.bash_aliases
    if ! grep -q PYTHON_ALIAS_ADDED /home/vagrant/.bash_aliases; then
      echo "# PYTHON_ALIAS_ADDED" >> /home/vagrant/.bash_aliases
      echo "alias python='python3'" >> /home/vagrant/.bash_aliases
    fi
  SHELL

  config.vm.provider "virtualbox" do |v|
    v.gui = false
    v.memory = 2048
  end

 end

