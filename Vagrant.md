# Vagrant
A login into the VM with `vagrant ssh` lets you interact with the Bash shell, but Ansible needs to connect to the VM via regular SSH. 
To achieve this you need to output the SSH configuration of Vagrant:
```
$ vagrant ssh-config
```

The output could look like this, although the important lines are the `hostname`, `user`, `port` and `IdentityFIle`
```
Host default 
HostName 127.0.0.1 
User vagrant 
Port 2222 
UserKnownHostsFile /dev/null 
StrictHostKeyChecking no 
PasswordAuthentication no 
IdentityFile C:/Users/basme/.vagrant.d/insecure_private_key 
IdentitiesOnly yes LogLevel FATAL
```

To connect to the VM use: 
```
$ ssh User@HostName -p Port \
  -i IdentityFile
$ ssh vagrant@127.0.0.1 -p 2222 \ -i .vagrant/machines/default/virtualbox/private_key
```

## Configuration Options 
### Port Forwarding and Private IP Addresses
>[!note]
>When starting a new Vagrant file by using `vagrant init` the default networking configuration allows you to reach the Vagrant box only via a SSH port that is forwarded from local host.  

Web applications listen on ports that we can not access. To work around this problem we can set up forwarding ports. For example, the application listens on port 80 inside the Vagrant machine, so you can configure Vagrant to forward port 8040 on your local machine to port 80 on the VM.
![[Vagrant Port forwarding.png]]

To configure port forwarding add the following in the `Vagrantfile`:
```
config.vm.network :forwarded_port, host: 8000, guest: 80 
config.vm.network :forwarded_port, host: 8443, guest: 443
```

It is also possible to assign the VM a private IP address that is only accessible from the host machine.
```
config.vm.network "private_network", ip: "192.168.33.10"
```
If we run a web server on the VM, we can access it via `http:// 192.168.33.10` with a browser.
## Creating Multiple VMs with Vagrant
To create multiple Vagrant machines create a new Vagrantfile:
```
Vagrant.configure("2") do |config|
# Use the same key for each machine
  config.ssh.insert_key = false
  config.vm.define "vagrant1" do |vagrant1|
	vagrant1.vm.box = "ubuntu/focal64"
	vagrant1.vm.network "forwarded_port", guest: 80, host: 8080
	vagrant1.vm.network "forwarded_port", guest: 443, host: 8443
  end
  config.vm.define "vagrant2" do |vagrant2|
	vagrant2.vm.box = "ubuntu/focal64"
	vagrant2.vm.network "forwarded_port", guest: 80, host: 8081
	vagrant2.vm.network "forwarded_port", guest: 443, host: 8444
  end
  config.vm.define "vagrant3" do |vagrant3|
	vagrant3.vm.box = "centos/8"
	vagrant3.vm.network "forwarded_port", guest: 80, host: 8082
	vagrant3.vm.network "forwarded_port", guest: 443, host: 8445
  end
end
```

After we started the VMs with `vagrant up` we inspect the ssh settings of them with:
```
$ vagrant ssh-config
```

We now modify the file `~/.ssh.config`
```
Host vagrant*
 Hostname 127.0.0.1
 User vagrant
 UserKnownHostsFile /dev/null
 StrictHostKeyChecking no
 PasswordAuthentication no
 IdentityFile ~/.vagrant.d/insecure_private_key
 IdentitiesOnly yes
 LogLevel FATAL
```
