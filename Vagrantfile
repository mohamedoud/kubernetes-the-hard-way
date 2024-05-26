hosts = [
    { hostname: "jumpbox", ip: "192.168.56.10", cpus: 1, memory: 512, storage: 10 },
    { hostname: "server", ip: "192.168.56.11", cpus: 1, memory: 2048, storage: 10 },
    { hostname: "node-0", ip: "192.168.56.12", cpus: 2, memory: 2048, storage: 10 },
    { hostname: "node-1", ip: "192.168.56.13", cpus: 2, memory: 2048, storage: 10 }
]

def configure_vm(config, hostname, ip, cpus, memory)
    config.vm.define hostname, autostart: true do |cfg|
        cfg.vm.hostname = hostname
        cfg.vm.network "private_network", ip: ip
        cfg.vm.provider "virtualbox" do |vb|
            vb.name = hostname # sets gui name for VM
            vb.customize ["modifyvm", :id, "--memory", memory, "--cpus", cpus, "--hwvirtex", "on"]
        end
    end
    end

Vagrant.configure("2") do |config|
    config.vm.box = "debian/bookworm64"
    hosts.each do |host|
        config.vm.disk :disk, size: host[:storage] * 1024, primary: true
        configure_vm(config, host[:hostname], host[:ip], host[:cpus], host[:memory])
    end
  end
  