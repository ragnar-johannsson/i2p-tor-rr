$setup = <<SCRIPT
    apt-get update
    apt-get install -y python-software-properties
    apt-add-repository -y ppa:i2p-maintainers/i2p
    apt-get update
    apt-get install -y i2p tor polipo ipvsadm privoxy
    ip addr add 172.31.0.1/24 dev eth0
    su - vagrant -c "i2prouter start && i2prouter stop"
    sed -i s/127.0.0.1/172.31.0.1/ /home/vagrant/.i2p/*.config
    su - vagrant -c "i2prouter start"
    echo "socksParentProxy = localhost:9050" > /etc/polipo/config
    echo "diskCacheRoot=\"\"" >> /etc/polipo/config
    echo "proxyAddress=172.31.0.1" >> /etc/polipo/config
    service polipo restart
    ipvsadm -A -t 172.20.172.20:8080 -s wrr
    ipvsadm -a -t 172.20.172.20:8080 -r 172.31.0.1:8123 -m -w 1
    ipvsadm -a -t 172.20.172.20:8080 -r 172.31.0.1:4444 -m -w 1
    ipvsadm -A -t 172.20.172.20:8090 -s wrr
    ipvsadm -a -t 172.20.172.20:8090 -r 172.31.0.1:8123 -m -w 1
    ipvsadm -a -t 172.20.172.20:8090 -r 172.31.0.1:4445 -m -w 1
    sed -i s/localhost:8118/172.20.172.20:8118/ /etc/privoxy/config
    echo "forward / 172.20.172.20:8080" >> /etc/privoxy/config
    echo "forward :443 172.20.172.20:8090" >> /etc/privoxy/config
    service privoxy restart
SCRIPT

Vagrant::Config.run do |config|
    config.vm.box = "precise64"
    config.vm.box_url = "http://files.vagrantup.com/precise64.box"
    config.vm.network :hostonly, "172.20.172.20"
    config.vm.provision :shell, :inline => $setup
end
