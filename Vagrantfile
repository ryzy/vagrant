VAGRANTFILE_API_VERSION = "2"
Vagrant.require_version ">= 1.7.0"

$script = <<SCRIPT
echo "DOCKER_OPTS=--host=tcp://0.0.0.0:2375" >> /run/flannel_docker_opts.env
systemctl restart docker
SCRIPT

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define "docker-generic-host"
  config.vm.hostname = "docker-generic-host"

  config.vm.box = 'AntonioMeireles/coreos-beta'
  config.vm.box_version = ">= 766.1.0"

  config.vm.provider :virtualbox do |v, override|
    override.v.network :private_network, ip: '192.168.88.8'
    v.gui = false
    v.customize ['modifyvm', :id, '--memory', 4096]
    v.customize ['modifyvm', :id, '--cpus', 8]
  end

  config.vm.provider :parallels do |v, override|
    v.customize ['set', :id, '--memsize', 4096]
    v.customize ['set', :id, '--cpus', 8]
    v.customize ['set', :id, '--adaptive-hypervisor', 'on']
  end

  config.vm.provision "shell", inline: $script, run: "always"
end
