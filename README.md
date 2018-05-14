docker testnet
==============

Run and manage your own local [I2P network](http://i2pd.website) with Docker.


Installing
----------

Install requirements and add your user to docker group ([security notes](https://docs.docker.com/engine/installation/linux/linux-postinstall/)):

    sudo apt install docker.io python3 python3-venv
    sudo gpasswd -a your-user docker
    newgrp docker

Clone the repo: 
    
    git clone https://github.com/majestrate/docker-testnet && cd docker-testnet

Create virtual environment and install the testnet files:

    python3 -m venv v && v/bin/pip install .


Build Testnet branch:

    git clone https://github.com/majestrate/i2pd -b loki-testnet i2pd-loki
    cd i2pd-loki
    make docker
    
Usage
-----

Read help message:

    v/bin/testnetctl -h
    
Start a network: 

    v/bin/testnetctl start

Or you may want to start a network with some nodes and floodfills:

    v/bin/testnetctl start --nodes 10 --floodfills 5

Add 5 floodfill nodes and 10 regular nodes:

    v/bin/testnetctl add 5 --floodfill
    v/bin/testnetctl add 10

Show network statistics overview:

    v/bin/testnetctl status

Show individual node information:

    v/bin/testnetctl inspect d34db33f1001
    
Remove couple of nodes:

    v/bin/testnetctl remove d34db33f1001 3f1001d34db3

Create I2P tunnel (options are specified exactly as `key=value` without spaces):

    v/bin/testnetctl create_tunnel d34db33f1001 test-tunnel type=http host=127.0.0.1 port=8888 keys=test.dat

Stop a network and quit:

    v/bin/testnetctl stop


Configuration
-------------

Takes environment variables for configuration:

    I2PD_IMAGE   -  docker image to use
    NETNAME      -  docker network name
    DEFAULT_ARGS -  default arguments for binary

