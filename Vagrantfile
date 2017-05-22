ENV["LC_ALL"] = "eS_ES.UTF-8"

Vagrant.configure("2") do |config|
    # Intentamos prevenir avisos 'stdin is not a tty'
    config.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"

    puts ""
    puts ""
    puts " \033[38;5;118m .----------------. \033[38;5;206m .----------------. \033[38;5;33m .----------------. "
    puts " \033[38;5;118m| .--------------. |\033[38;5;206m| .--------------. |\033[38;5;33m| .--------------. |"
    puts " \033[38;5;118m| | ____   ____  | |\033[38;5;206m| |      __      | |\033[38;5;33m| |   ______     | |"
    puts " \033[38;5;118m| ||_  _| |_  _| | |\033[38;5;206m| |     /  \\     | |\033[38;5;33m| |  |_   __ \\   | |"
    puts " \033[38;5;118m| |  \\ \\   / /   | |\033[38;5;206m| |    / /\\ \\    | |\033[38;5;33m| |    | |__) |  | |"
    puts " \033[38;5;118m| |   \\ \\ / /    | |\033[38;5;206m| |   / ____ \\   | |\033[38;5;33m| |    |  ___/   | |"
    puts " \033[38;5;118m| |    \\ ' /     | |\033[38;5;206m| | _/ /    \\ \\_ | |\033[38;5;33m| |   _| |_      | |"
    puts " \033[38;5;118m| |     \\_/      | |\033[38;5;206m| ||____|  |____|| |\033[38;5;33m| |  |_____|     | |"
    puts " \033[38;5;118m| |              | |\033[38;5;206m| |              | |\033[38;5;33m| |              | |"
    puts " \033[38;5;118m| '--------------' |\033[38;5;206m| '--------------' |\033[38;5;33m| '--------------' |"
    puts " \033[38;5;118m '----------------' \033[38;5;206m '----------------' \033[38;5;33m '----------------' "
    puts ""
    puts "  \033[38;5;118mVagrant             \033[38;5;206mAnsible             \033[38;5;33mPrestashop"
    puts ""
    puts "  \033[0mv: 1.0.0"
    puts "  \033[0mBy: Carlos Longarela"
    puts ""
    puts "  \033[38;5;220mDocs:       https://galaxy.ansible.com/CarlosLongarela/prestashop/"
    puts ""
    puts ""
    puts "\033[0m"
    # Box
    config.vm.box = "ubuntu/xenial64"

    # Configuración de red
    # Para poder acceder por nombre debemos tener instalado Vagrant::Hostsupdater
    # Instalamos con $ vagrant plugin install vagrant-hostsupdater
    # Actualizamos con $ vagrant plugin update vagrant-hostsupdater
    config.vm.network :private_network, ip: "192.168.50.69"
    config.vm.hostname = "prestashop.test"

    # Si queremos mapear algún puerto
    #config.vm.network "forwarded_port", guest: 80, host: 8383
    #config.vm.network "forwarded_port", guest: 3306, host: 3366

    # Directorios compartidos
    config.vm.synced_folder "./www/public", "/home/webs/prestashop.test/public",
        owner: "www-data",
        group: "www-data",
        mount_options: ["dmode=777,fmode=777"],
        create: true

    config.vm.synced_folder "./www/logs", "/home/webs/prestashop.test/logs",
        owner: "www-data",
        group: "www-data",
        mount_options: ["dmode=777,fmode=777"],
        create: true

    # Configuración específica del Provider
    config.vm.provider "virtualbox" do |vb|
        vb.memory = 1024
        vb.cpus = 2
    end

    # Ejecutamos Ansible desde la máquina virtual para provisionar el software
    config.vm.provision "ansible_local" do |ansible|
        ansible.playbook = "provisioning/prestashop.yml"
        ansible.galaxy_role_file = "provisioning/requirements.yml"
    end
end
