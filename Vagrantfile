Vagrant.configure("2") do |config|

  config.vm.box = "bento/ubuntu-20.04"

  config.vm.network "private_network", ip: "172.30.1.55"
  config.vm.synced_folder ".", ""

  config.vm.provision "file", source: "./.djengu/.production_toolbox/server_setup.sh", destination: "/home/vagrant/server_setup.sh"
  config.vm.provision "file", source: "./.djengu/.production_toolbox/caddy", destination: "/home/vagrant/"

  config.vm.provision "shell", inline: <<-SHELL
    mv /home/vagrant/caddy/ /
    mkdir /root/.ssh/
    touch /root/.ssh/authorized_keys
    /home/vagrant/server_setup.sh
    cd /caddy/ && docker-compose -f docker-compose.caddy.yml up --build -d
    usermod -aG docker vagrant
  SHELL
end
