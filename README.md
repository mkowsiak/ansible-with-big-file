# ansible-with-big-file

This sample shows how to make `anisble-composer` fail while building large images.

# Reproducing the issue (macOS) 

## Install Ansible Container

    $ python2.7 -m ensurepip --default-pip
    $ sudo pip install virtualenv
    $ virtualenv venv
    $ source venv/bin/activate
    $ pip install ansible
    $ pip install ansible-container[docker]
    $ pip install docker==2.7.0
    
## Clone the repo and build image
    $ git clone https://github.com/mkowsiak/ansible-with-big-file.git
    $ cd ansible-with-big-file
    $ ansible-container build
    
    # at some point, you will get ReadTimeout (timeout=60)
    
# How to fix the issue?

## Get ansible container from sources

    $ git clone https://github.com/ansible/ansible-container.git
    $ cd ansible-container
    $ pip install -e .[docker]
    
    # Modify file: ansible-container/container/docker/templates/conductor-local-dockerfile.j2
    $ echo "" >> ansible-container/container/docker/templates/conductor-local-dockerfile.j2
    $ echo "ENV DOCKER_CLIENT_TIMEOUT=600" >> ansible-container/container/docker/templates/conductor-local-dockerfile.j2
    
    # Create image. This time, using custom conductor
    $ cd ansible-with-big-file
    $ ansible-container build --no-cache
