
# Vagrantfile
Modify the Vagrantfile to look like this:
```
Vagrant.configure(2) do |config| 
# start a ubuntu/focal64 server
config.vm.box = "ubuntu/focal64" 
config.vm.hostname = "testserver" 
config.vm.network "forwarded_port",
# map ssh port on localhost 2202 to 22 on VM
id: 'ssh', guest: 22, host: 2202, host_ip: "127.0.0.1", auto_correct: false
 config.vm.network "forwarded_port",
 # map port 8080 on localhost to 80 on VM
 id: 'http', guest: 80, host: 8080, host_ip: "127.0.0.1"
 config.vm.network "forwarded_port",
 id: 'https', guest: 443, host: 8443, host_ip: "127.0.0.1"
 # disable updating guest additions
 if Vagrant.has_plugin?("vagrant-vbguest")
 config.vbguest.auto_update = false
 end 
 config.vm.provider "virtualbox" do |virtualbox|
 virtualbox.name = "ch03"
 end
end
```

Start Vagrant with `vagrant up`.

# Interacting with the VM
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
### Port Forwarding
>[!note]
>When starting a new Vagrant file by using `vagrant init` the default networking configuration allows you to reach the Vagrant box only via a SSH port that is forwarded from local host.  

Port forwarding between the VM and the hypervisor can be configured to expose specific ports that can then be accessed.

![[Vagrant Port forwarding.png]]

For example web applications listens on port 80 inside the Vagrant machine, so it can be configured to forward port 8080 on the local machine to port 80 on the VM.

To configure port forwarding add the following in the `Vagrantfile`:
```
config.vm.network :forwarded_port, host: 8080, guest: 80 
config.vm.network :forwarded_port, host: 8443, guest: 443
```

### Private IP Addresses
It is also possible to assign the VM a private IP address that is only accessible from the host machine.
```
config.vm.network "private_network", ip: "192.168.33.10"
```
If we run a web server on the VM, we can access it via `http:// 192.168.33.10` with a browser.

### Agent Forwarding
Agent forwarding is used when checking a remote Git repository over SSH
```
VAGRANTFILE_API_VERSION = "2" Vagrant.configure(VAGRANTFILE_API_VERSION) do |config| 
config.ssh.forward_agent = true 
end
```

### Docker Provisioner
Vagrant can configured to create a VM, install Docker or Podman and run a container automatically
```
Vagrant.configure("2") do |config| 
	config.vm.box = "ubuntu/focal64" 
	config.vm.provision "docker" do |d| 
	    d.run "nginx"
	end
end
```
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

# Provisioner
*Provisioners* are tolls that can be used to configure a VM after it was started up and can be used with shell scripts, Chef, Puppet, Salt and CFEngine.
For example you can install Ansible on a VM and use it as a provisioner.  
```
VAGRANTFILE_API_VERSION = "2" 
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config| 
	config.vm.box = "ubuntu/xenial64" 
	# Install Ansible and provision "playbook.yaml"
	config.vm.provision "ansible_local" do |ansible| 
		ansible.compatibility_mode = "2.0" 
		ansible.galaxy_role_file = "roles/requirements.yml"
		ansible.galaxy_roles_path = "roles" 
		ansible.playbook = "playbook.yml" 
		ansible.verbose = "vv" 
	end 
end
```
# Command-Line
### Killing VMs
To destroy a VM and remove it use:
```
$ vagrant destroy -f
```

