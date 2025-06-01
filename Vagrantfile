# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Base box
  config.vm.box = "ubuntu/jammy64"

  # VM 1: jenkins-sonar
  config.vm.define "jenkins-sonar" do |js|
    js.vm.hostname = "jenkins-sonar"
    js.vm.network "private_network", ip: "192.168.56.10"

    js.vm.provider "virtualbox" do |vb|
      vb.name = "jenkins-sonar"
      vb.memory = 4096
      vb.cpus = 2
    end

    js.vm.provision "shell", inline: <<-SHELL
      #!/bin/bash
      sudo apt update -y
      #sudo apt upgrade -y
      sudo mkdir -p /etc/apt/keyrings
      wget -O - https://packages.adoptium.net/artifactory/api/gpg/key/public | sudo tee /etc/apt/keyrings/adoptium.asc
      echo "deb [signed-by=/etc/apt/keyrings/adoptium.asc] https://packages.adoptium.net/artifactory/deb $(awk -F= '/^VERSION_CODENAME/{print$2}' /etc/os-release) main" | sudo tee /etc/apt/sources.list.d/adoptium.list
      sudo apt update -y
      sudo apt install temurin-17-jdk -y
      /usr/bin/java --version

      curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
      echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
      sudo apt-get update -y
      sudo apt-get install jenkins -y
      sudo systemctl start jenkins
      sudo systemctl enable jenkins
      sudo systemctl status jenkins
    SHELL
  end

  # VM 2: grafana
  config.vm.define "grafana" do |g|
    g.vm.hostname = "grafana"
    g.vm.network "private_network", ip: "192.168.56.11"
    g.vm.network "forwarded_port", guest: 3000, host: 3000

    g.vm.provider "virtualbox" do |vb|
      vb.name = "grafana"
      vb.memory = 1024
      vb.cpus = 1
    end

    g.vm.provision "shell", inline: <<-SHELL
      sudo apt update
      sudo apt install -y apt-transport-https software-properties-common wget curl gnupg

      sudo mkdir -p /etc/apt/keyrings
      curl -fsSL https://packages.grafana.com/gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/grafana.gpg
      echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://packages.grafana.com/oss/deb stable main" | sudo tee /etc/apt/sources.list.d/grafana.list

      sudo apt update
      sudo apt install -y grafana
      sudo systemctl enable grafana-server
      sudo systemctl start grafana-server
    SHELL
  end
end

