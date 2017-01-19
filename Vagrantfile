require 'yaml'

conf = YAML.load_file(File.dirname(__FILE__) + '/config.yml')

Vagrant.configure("2") do |config|

  config.vm.box = conf['vagrant_box']

  config.vm.network "private_network", ip: conf['private_ip']

  config.vm.hostname = conf['vagrant_hostname']

  # SSH options.
  config.ssh.insert_key = false
  config.ssh.forward_agent = true

  # config.vm.synced_folder HOST_HOME, HOST_HOME_SHARE
  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.provider "virtualbox" do |v|
    v.gui = false
    v.memory = conf['vagrant_memory']
    v.cpus = conf['vagrant_cpus']
  end

  config.vm.provision "ansible", run: conf['vagrant_provision'] do |a|
    a.playbook = "./provisioning/playbook.yml"
  end

end
