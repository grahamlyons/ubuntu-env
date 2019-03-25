# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.box = 'ubuntu/bionic64'

  config.vm.network 'private_network', ip: '10.10.10.30'

  config.vm.synced_folder File.join(ENV['HOME'], 'workspace'), '/home/vagrant/workspace/'

  config.vm.provision 'shell', inline: 'apt-get update'
  config.vm.provision 'shell', inline: 'apt-get install -y apt-transport-https ca-certificates curl software-properties-common'
  config.vm.provision 'shell', inline: 'curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -'
  config.vm.provision "shell", inline: 'add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) edge"'
  config.vm.provision 'shell', inline: 'apt-get update'
  config.vm.provision 'shell', inline: 'apt-get install -y docker-ce'
  config.vm.provision 'shell', inline: 'systemctl enable --now docker'
  config.vm.provision 'shell', inline: 'usermod -aG docker vagrant'             

  config.vm.provision 'shell', inline: 'apt-get install -y vim tmux'

  config.vm.provision 'shell', inline: 'apt-get upgrade -y'

  config.vm.provision 'file', source: '~/.ssh/id_rsa', destination: '~/.ssh/id_rsa'
  config.vm.provision 'file', source: '~/.vimrc', destination: '~/.vimrc'
  config.vm.provision 'file', source: '~/.secrets', destination: '~/.secrets'
  config.vm.provision 'shell',
    privileged: false,
    inline: 'if [ "$(grep -v secrets ~/.bash_aliases)" ]; then echo "source ~/.secrets" >> ~/.bash_aliases; fi'             
end
