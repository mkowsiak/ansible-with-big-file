$ python2.7 -m ensurepip --default-pip
$ virtualenv venv
$ source venv/bin/activate
$ pip install ansible
$ pip install ansible-container[docker]
$ pip install docker==2.7.0
$ ansible-container build
