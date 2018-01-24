## Introduction
This repository code holds some example code for how to use Ansible to target a set of remote hosts to download a file, explode it and verify a thing or two. 

A simple `Vagrantfile` here to potentially be used as the environment in which to use this code.

## Setting up a Virtualenv
```
virtualenv venv
. venv/bin/activate
pip install --upgrade setuptools pip
pip install -r requirements.txt
```

## Configuring your hosts file
Uncomment a given host entry or entries and modify them to reflect the IP address(es) of the target host(s). For example:
```
[targets]
#host0 ansible_host=a.b.c.d
#host1 ansible_host=a.b.c.d
#host2 ansible_host=a.b.c.d

could be changed to:

[targets]
host0 ansible_host=1.1.1.1
host1 ansible_host=2.2.2.2
host2 ansible_host=3.3.3.3
```

## Copy your key to the target hosts
```
. venv/bin/activate
ansible-playbook --ask-pass --user <remote user> copykey.yml

ie.

ansible-playbook --ask-pass --user frank copykey.yml
```
where `remote user` is the name of the user on the target host(s) that you will use to connect with. You will be prompted to enter the password of the `remote user`.

## Modify the ansible.cfg file to reflect the remote user
Modify the `remote_user` entry in the `ansible.cfg` file to reflect the `remote user` outlined above. For example:
```
remote_user: FIXME

ie.

remote_user: frank
```

## Run the simple.yml playbook
```
. venv/bin/activate
ansible-playbook simple.yml
```
To avoid warnings like:
```
 [WARNING]: Consider using get_url or uri module rather than running curl

and

 [WARNING]: Consider using unarchive module rather than running tar
```
have a look at the `simple-ansible.yml` playbook for a slightly more `Ansible`-ish way of doing things.

