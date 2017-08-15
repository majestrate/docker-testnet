docker testnet
==============

Run and manage your own local [I2P network](http://i2pd.website) with Docker.


Installing
----------

Install requirements and add your user to docker group ([security notes](https://docs.docker.com/engine/installation/linux/linux-postinstall/)):

    sudo apt install docker.io python3 python3-venv
    sudo gpasswd -a your-user docker

Clone the repo: 
    
    git clone https://github.com/l-n-s/docker-testnet && cd docker-testnet

Build docker images:

    ./build/build_images.sh 

Create virtual environment and install:

    python3 -m venv venv && source venv/bin/activate
    pip install .


Usage
-----

Run with `testnet` command:

    testnet

Read help message:

    testnet> help
    
Start a network, this command creates 1 floodfill node and a reseed server: 

    testnet> start

Add 5 floodfill nodes and 10 regular nodes:

    testnet> add 5 ff
    testnet> add 10

Show network statistics overview:

    testnet> stats

Show individual node information:

    testnet> inspect d34db33f1001
    
Remove couple of nodes:

    testnet> remove d34db33f1001 3f1001d34db3

Create I2P tunnel (options are specified exactly as `key=value` without spaces):

    testnet> create_tunnel d34db33f1001 test-tunnel type=http host=127.0.0.1 port=8888 keys=test.dat

Stop a network and quit:

    testnet> stop
    testnet> quit


Configuration
-------------

Takes environment variables for configuration:

    I2PD_IMAGE   -  docker image to use
    NETNAME      -  docker network name
    DEFAULT_ARGS -  default arguments for binary

