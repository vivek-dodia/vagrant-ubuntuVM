Vagrant.configure('2') do |config|
  (1..1).each do |i|
    config.vm.define "ubuntuTEST" do |machine|
      machine.vm.box = 'ubuntu/focal64'
      machine.vm.hostname = "ubuntuTEST"
      machine.vm.provider "virtualbox" do |vb|
        vb.name = "ubuntuTEST-#{i}"
        vb.cpus = 8
        vb.memory = '8192'
      end

      # Provisioning block to install packages
      machine.vm.provision "shell", inline: <<-SHELL
        # Update and upgrade the system
        sudo apt-get update
        sudo apt-get upgrade -y

        # Install dependencies
        sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common lsb-release

        # Install traceroute
        sudo apt-get install -y traceroute

        # Install Tailscale
        curl -fsSL https://tailscale.com/install.sh | sh

        # Add Docker’s official GPG key
        curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

        # Set up the stable repository
        sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

        # Update apt package index again after adding Docker repo
        sudo apt-get update

        # Install Docker Engine and component packages
        sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

        #  UFW
        sudo apt-get install ufw -y

        # Nano
        sudo apt-get install nano -y

        # Install Containerlab
        bash -c "$(curl -sL https://get.containerlab.dev)"

        # Post-installation steps to manage Docker as a non-root user
        sudo usermod -aG docker vagrant

        # Apply new group membership (you would need to logout/login for this to take effect, or just reboot the VM)
        # Note: The VM will need to be rebooted for docker group changes to take effect.
      SHELL
    end
  end
end
