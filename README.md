# Chef notes

## apply particular recipe
chef-apply file_name.rp

## generates new cookbook
chef generate cookbook NAME_OF_THE_COOKBOOK

## generates new template inside given cookbook
chef generate template COOKBOOK_NAME TEMPLATE_FILE_NAME

## write recipe in the file 'COOKBOOK_NAME/recipes/default.rba'

## run cookbook
chef-client --local-mode --runlist 'recipe[COOKBOOK_NAME]'

## download cookbook from supermaket.chef.io
knife cookbook site download COOKBOOK_NAME_IN_supermarket.chef.io

## upload cookbook to Chef server
knife cookbook upload COOKBOOK_NAME

## bootstrap node
knife bootstrap NODE_IP_ADDRESS --ssh-user USER --ssh-password 'PASSWORD' --sudo -use-sudo-password --node-name cnode1 --run-list 'recipe[COOKBOOK_NAME]'

## node list (inside folder where is unzipped starter kit)
knife node list

## particular node
knife node show NODE_NAME

