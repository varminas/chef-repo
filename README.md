# Chef notes

Apply particular recipe
```sh
$ chef-apply file_name.rp
```

Generates new cookbook
```sh
$ chef generate cookbook NAME_OF_THE_COOKBOOK
```

Generates new template inside given cookbook
```sh
$ chef generate template COOKBOOK_NAME TEMPLATE_FILE_NAME
```

Write recipe in the file 'COOKBOOK_NAME/recipes/default.rba'

Run cookbook
```sh
$ chef-client --local-mode --runlist 'recipe[COOKBOOK_NAME]'
```

Download cookbook from supermaket.chef.io
```sh
$ knife cookbook site download COOKBOOK_NAME_IN_supermarket.chef.io
```

Ipload cookbook to Chef server
```sh
$ knife cookbook upload COOKBOOK_NAME
```

Bootstrap node
```sh
$ knife bootstrap NODE_IP_ADDRESS --ssh-user USER --ssh-password 'PASSWORD' --sudo -use-sudo-password --node-name cnode1 --run-list 'recipe[COOKBOOK_NAME]'
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

# Berks
Upload cookbooks and dependencies to the Chef server
```sh
$ SSL_CERT_FILE='.chef/trusted_certs/chef-server_test.crt' berks upload
```

Upload role to Chef server
```sh
$ knife role from file roles/web.json
```

# Kitchen
todo
