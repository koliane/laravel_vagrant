Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  
  config.vm.network "forwarded_port", guest: 80, host: 80, host_ip: "127.0.0.1"
  
  config.vm.provider "virtualbox" do |vb|    
    vb.memory = "8192"
    vb.cpus = 4
  end
  
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt update && sudo apt upgrade -y
    sudo update-alternatives --install /usr/bin/python python /usr/bin/python3 2
    sudo apt install python3-pip -y
    sudo pip3 install ansible
    sudo apt install git -y
    ssh-keygen -q -t rsa -N '' -f ~/.ssh/id_rsa <<<y >/dev/null 2>&1
    git clone https://github.com/koliane/laravel_ansible.git /tmp/ansible
    ansible-playbook /tmp/ansible/playbook.yaml --extra-vars "project_name=laravel_project db_name=laravel_db db_user_name=laravel db_user_password=12345678"
  SHELL
  
end
