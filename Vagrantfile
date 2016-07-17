# Vagrant - Dev Env
Vagrant.configure(2) do |config|

    # User that will be created with sudo rights on the VM.
    if ARGV[0] == "up" or ARGV[0] == "provision"
        uid   = 4000
        uname = 'admin'
        gid   = 4000
        gname = 'devs'
        shell = '/bin/bash'
        puts "Insert password for user '#{uname}' in guest machines: "
        `stty -echo`
        pwd = $stdin.gets.chomp
        pwd = `perl -e 'print crypt("#{pwd}", "salt")'`
        `stty echo`
    end

    # Dev Env
    config.vm.define "dev" do |dev|
        dev.vm.box = "ubuntu/trusty64"
        dev.vm.provider "virtualbox" do |v|
            v.memory = 2048
        end
        dev.vm.hostname = "dev"
        dev.vm.network "private_network", ip: "192.168.33.101"
        dev.vm.provision "shell", inline: "groupadd -g #{gid} #{gname}"
        dev.vm.provision "shell", inline: "useradd -u #{uid} -g #{gid} -G sudo -p #{pwd} -m -s #{shell} #{uname}"
        dev.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "/tmp/authorized_keys"
        dev.vm.provision "shell", inline: "mkdir -p /home/#{uname}/.ssh"
        dev.vm.provision "shell", inline: "mv /tmp/authorized_keys /home/#{uname}/.ssh/authorized_keys"
        dev.vm.provision "shell", inline: "chown -R #{uid}:#{gid} /home/#{uname}/.ssh"
    end

end
