# Chef notes
+ **chef-apply** - runs a single recipe from the command line
+ **chef-client** - uploads policy on your node. Typically downloads and runs the latest Chef code from the Chef server. However, possible to run in the *local mode*
+ **kitchen** - enabled to run cookbooks in a temporary environment.
	Steps: *kitchen create* -> *kitchen converge* -> *kitchen login* -> *verify* -> *kitchen destroy*
+ **knife** - enables you to communicate with the Chef server from your workstation.
+ **berks** - dependency management tool

Apply particular recipe
```sh
$ chef-apply file_name.rp
```
or
```sh
$ chef-client --local-mode hello.rb
```
# Cookbooks
To reference a cookbook from inside another, put it's name into **metadata.rb** file, e.g. put *depends 'apt', '~> 4.0'*, then include it into recipe recipes/default.rb *include_recipe 'apt::default'*

Create a cookbook
```sh
$ chef generate cookbook cookbooks/learn_chef_apache
```

Generates new template inside given cookbook
```sh
$ chef generate template cookbooks/learn_chef_apache2 index.html
```

Write recipe in the file *'COOKBOOK_NAME/recipes/default.rba'*

Run the cookbook
```sh
$ sudo chef-client --local-mode --runlist 'recipe[learn_chef_apache2]'
```
Create the recipe
```sh
$ chef generate recipe cookbooks/awesome_customers_ubuntu firewall
```
Create the custom attributes file
```sh
$ chef generate attribute cookbooks/awesome_customers_ubuntu default
```

#Knife
Use file **./chef/knife.rb** for Knife configuration
Download cookbook from **supermaket.chef.io**
```sh
$ knife cookbook site download COOKBOOK_NAME_IN_supermarket.chef.io
```

Upload cookbook to the Chef server
```sh
$ knife cookbook upload COOKBOOK_NAME
```

Bootstrap node
```sh
$ knife bootstrap NODE_IP_ADDRESS --ssh-user USER --ssh-password 'PASSWORD' --sudo -use-sudo-password -N cnode1 --run-list 'recipe[COOKBOOK_NAME]' -E ENVIRONMENT_NAME -V
```

Node list (inside folder where is unzipped starter kit)
```sh
$ knife node list
```

Particular node
```sh
$ knife node show NODE_NAME
```

Upload cookbook to node
```sh
knife ssh localhost --ssh-port 2200 'sudo chef-client' --manual-list --ssh-user vagrant --identity-file /home/vytautas/learn-chef/chef-server/.vagrant/machines/node1-ubuntu/virtualbox/private_key
```
```sh
knife ssh 'name:NODE_NAME' 'sudo chef-client' --ssh-user root --identity-file ~/.ssh/id_rsa --attribute ipaddress --run-list='cookbook[COOKBOOK_NAME]'
```

# Berks
Set up a file named **Berksfile.lock** that helps Test Kitchen manage dependent cookbooks
```sh
$ berks install
```
Upload cookbooks and dependencies to the Chef server
```sh
$ SSL_CERT_FILE='.chef/trusted_certs/chef-server_test.crt' berks upload
```

Upload role to Chef server
```sh
$ knife role from file roles/web.json
```

# Test Kitchen
Command *chef generate cookbook* which creates cookbooks, creates file named **.kitchen.yml**
provisioner *chef_zero* enables you to mimic a Chef server environment on the local machine

## Create the Test Kitchen instance
See what's in the kitchen:
```sh
$ kitchen list
```
Create the instance
```sh
$ kitchen create
```
## Converge
```sh
$ kitchen converge
```
Test kitchen runs *chef-client* on the instance. When *chef-client* run completes cuccessfully, Test Kitchen exits with code 0 (to check exit code run *echo $?*)
## Verify
Login using ssh
```sh
$ kitchen login
```
Execute single command
```sh
$ kitchen exec -c 'wget -qO- localhost
```
## Destroy
Destroy instance
```sh
$ kitchen destroy
```

# Vagrant
Check Vagrant version
```sh
$ vagrant --version
```
Download specific Vagrant box
```sh
$ vagrant box add bento/ubuntu-14.04 --provider=virtualbox
```
Create configuration file named **Vagrantfile**
```sh
$ vagrant init bento/ubuntu-14.04
```
Bring up an instance (create and configure VM instance)
```sh
$ vagrant up
```
Connect to the instance
```sh
vagrant ssh
```

Cleaning up
```sh
$ vagrant destroy --force
```
