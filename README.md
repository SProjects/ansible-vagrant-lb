# Setting up a loadbalancer

## Pre-requisites
- Vagrant
- VirtualBox

## Usage
- Run `vagrant init`
- Run `vagrant up`
- Run `vagrant ssh acs` to log into the "ansible control server (acs)"
- (One time command) Run `ssh-keygen`
- (One time command) Copy the public key to each of the other hosts in the `~/.ssh/authosized_hosts` file
- Run `ansible-playbook --private-key=~/.ssh/id_rsa site.yaml`
- Load `192.168.33.20` in the browser and refresh several time. The site should load a blue and green page which the load balancer is loading in turn.