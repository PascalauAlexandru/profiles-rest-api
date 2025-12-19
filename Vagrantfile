# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.box_version = "~> 20200304.0.0"

  config.vm.network "forwarded_port", guest: 8000, host: 8000

  # --- SECȚIUNEA NOUĂ PENTRU DEPANARE ---
  config.vm.provider "virtualbox" do |vb|
     # Activează "monitorul" ca să vedem erorile la pornire
     # Alocă 2GB RAM ca să nu se blocheze
     vb.memory = "2048"
     # Alocă 2 procesoare (opțional, ajută la viteză)
     vb.cpus = 2
  end
  # --------------------------------------

  config.vm.provision "shell", inline: <<-SHELL
    systemctl disable apt-daily.service
    systemctl disable apt-daily.timer

    sudo apt-get update
    sudo apt-get install -y python3-venv zip
    touch /home/vagrant/.bash_aliases
    if ! grep -q PYTHON_ALIAS_ADDED /home/vagrant/.bash_aliases; then
      echo "# PYTHON_ALIAS_ADDED" >> /home/vagrant/.bash_aliases
      echo "alias python='python3'" >> /home/vagrant/.bash_aliases
    fi
  SHELL
end