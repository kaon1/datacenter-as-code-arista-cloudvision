# datacenter-as-code-arista-cloudvision
Using Ansible to deploy a Data Center as Code  solution when using an Arista Datacenter Managed by Cloudvision

![](datacenter-as-code/pics/DCaC%20-%20Front.png)

## About
Fully deploy and manage an Arista Datacenter Buildout
Use ContainerLab to deploy an identical staging environment
Use Ansible to:
 - Render Configs
 - Push up to Arista Cloudvision
 - Create Change Control
 - Run post test validations

## Prepping Server Env

### Install Python3.9
- sudo yum install epel-release
- sudo yum install python-pip
- sudo yum install gcc openssl-devel bzip2-devel libffi-devel zlib-devel
- wget https://www.python.org/ftp/python/3.9.6/Python-3.9.6.tgz
- tar -xvf Python-3.9.6.tgz
- cd Python-3.9.6
- ./configure
- sudo make
- sudo make altinstall

### Create VENV
- python3.9 -m pip install --user --upgrade pip
- python3.9 -m venv /home/py39venv_daac
- source /home/py39venv_daac/bin/activate

### Clone Repo
- cd /home
- git clone ...
- cd datacenter-as-code-arista-cloudvision

### Install Deps
- /home/py39venv_daac/bin/python3.9 -m pip install --upgrade pip
- pip install -r requirements.txt
- ansible-galaxy install -r requirements.yml
- export NETBOX_TOKEN=__token__
- create vault.yml (ansible-vault create)

### Example Runs
- ansible-playbook -i netbox_dynamic_inventory.yml dcac-deploy.yml --ask-vault-pass -e "deploy_hosts=all" --tags generate_config
- post validate run example ansible-playbook -i netbox_dynamic_inventory.yml --ask-vault-pass -e "deploy_hosts=all" post-change-validate.yml 

![](datacenter-as-code/pics/DCaC%20-%20pipeline.png)

![](datacenter-as-code/pics/staging-build.png)