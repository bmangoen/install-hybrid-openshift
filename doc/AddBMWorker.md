## TO DO :)
In this section we will see how to deploy the new server using
1. need to install the library : https://github.com/HewlettPackard/oneview-ansible
exemple of scipt can be found https://github.com/NicolasO/ocp-on-synergy.git


# Pre-requisit

## Conda Installation for Oneview:
Full documentation is here :
https://docs.anaconda.com/anaconda/install/linux/

### Installation Package

    RedHat	yum install libXcomposite libXcursor libXi libXtst libXrandr alsa-lib mesa-libEGL libXdamage mesa-libGL libXScrnSaver


#### Enter the following to install Anaconda for Python 3.7:
    bash ~/Downloads/Anaconda3-2019.10-Linux-x86_64.sh

say Yes to all


## Managing environements
https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html

### Create environements
    conda create -n oneview-p3.6 python=3.6

### Check list of environements
    conda env list

### Activate the environment
    conda activate oneview-p3.6

### install oneview ansible

    git clone https://github.com/HewlettPackard/oneview-ansible.git
    cd oneview-ansible/
    pip install -r requirements.txt


### Avtivate environement Variables
    echo $CONDA_PREFIX
    cd /root/anaconda3/envs/oneview-p3.6
    mkdir -p ./etc/conda/activate.d
    mkdir -p ./etc/conda/deactivate.d
    touch ./etc/conda/activate.d/env_vars.sh
    touch ./etc/conda/deactivate.d/env_vars.sh
#### edit the env_vars
    cat ./etc/conda/activate.d/env_vars.sh
    #!/bin/sh

    export ANSIBLE_LIBRARY=/root/oneview-ansible/library
    export ANSIBLE_MODULE_UTILS=/root/oneview-ansible/library/module_utils/
    (oneview-p3.6) [root@lab-ansible oneview-p3.6]# cat ./etc/conda/deactivate.d/env_vars.sh
    #!/bin/sh

    unset export ANSIBLE_LIBRARY
    unset ANSIBLE_MODULE_UTILS

#### Edit the hosts file
    cd /root/oneview-ansible
    [all]
    localhost

    [all:vars]
    ansible_python_interpreter=/root/anaconda3/envs/oneview-p3.6/bin/python3.6


### test the integration  
    cd ~
    cd oneview-ansible/
    ansible-playbook -i ../inventory/hosts nico_oneview_server_profile_facts.yml
