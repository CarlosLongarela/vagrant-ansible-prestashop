Vagrant.configure("2") do |config|
    # Try to prevent 'stdin is not a tty' warnings
    config.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"

    # Box
    config.vm.box = "ubuntu/xenial64"

    # Network-specific configuration
    config.vm.hostname = "cl-prestashop"

    config.vm.network "forwarded_port", guest: 80, host: 8383
    config.vm.network "forwarded_port", guest: 3306, host: 3366

    # Shared directory
    config.vm.synced_folder "./www/pscode", "/var/www/modules/moduloejemplo",
        owner: "www-data",
        group: "www-data",
        mount_options: ["dmode=775,fmode=664"],
        create: true

    # Provider-specific configuration
    config.vm.provider "virtualbox" do |vb|
        vb.memory = 1024
        vb.cpus = 2
    end

    # Provisioner-specific configuration
    Vagrant.configure("2") do |config|
    # Run Ansible from the Vagrant VM
    config.vm.provision "ansible_local" do |ansible|
        ansible.playbook = "provisioning/prestashop.yml"
    end
end
