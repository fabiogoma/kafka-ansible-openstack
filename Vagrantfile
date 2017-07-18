zookeeper_boxes = %w(zookeeper1 zookeeper2 zookeeper3)
kafka_boxes = %w(kafka1 kafka2 kafka3)

Vagrant.configure('2') do |config|
  config.ssh.username = 'centos'
  config.ssh.private_key_path = '/home/fabiom/study/openstack/ing/keys/fabio.pem'
  config.ssh.pty = true
  # config.vm.synced_folder "/vagrant", ".", disabled: true
  config.vm.synced_folder '.', '/home/vagrant/sync', disabled: true

  config.vm.provider :openstack do |os, override|
    override.nfs.functional = false
    os.openstack_auth_url = 'http://openstack:5000/v2.0/tokens'
    os.username           = 'fabio'
    os.password           = ENV['OS_PASSWORD']
    os.tenant_name        = 'GMTT'
    os.flavor             = 'm1.medium'
    os.image              = 'CentOS'
    os.floating_ip_pool   = ['public-network']
    os.keypair_name       = 'fabio'
    os.networks           = ['private-network']
    os.security_groups    = ['default']
  end

  zookeeper_boxes.each_with_index do |box, index|
    config.vm.define box.to_s do |node|
      node.vm.hostname = box.to_s
      node.vm.provision 'ansible' do |ansible|
        ansible.limit = box.to_s
        ansible.verbose = false
        ansible.extra_vars = { 'zookeeper_server_list' => zookeeper_boxes, 'server_id' => index }
        ansible.playbook = 'provisioning/zookeeper-playbook.yml'
      end
    end
  end

  kafka_boxes.each_with_index do |box, index|
    config.vm.define box.to_s do |node|
      node.vm.hostname = box.to_s
      node.vm.provision 'ansible' do |ansible|
        ansible.limit = box.to_s
        ansible.verbose = false
        ansible.extra_vars = { 'zookeeper_server_list' => zookeeper_boxes, 'server_id' => index }
        ansible.playbook = 'provisioning/kafka-playbook.yml'
      end
    end
  end

end 
