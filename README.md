# Ansible Role Sentry Example

This repository is a [Ansible Role Sentry](https://github.com/harobed/ansible-role-sentry) usage demonstration.

Use this repository to install Sentry in Ubuntu VM managed by [Vagrant](https://www.vagrantup.com/).

## Prerequisite

- Python 3 (tested with `3.7.1`)
- Virtualenv
- Virtualbox
- Vagrant
- [vagrant-hostmanager](https://github.com/devopsgroup-io/vagrant-hostmanager) plugin

On OSX, execute this command with [brew](https://brew.sh/index_fr.html) to install this prerequisite :

```sh
$ brew install python3
$ pip install virtualenv==16.0.0
$ brew cask install vagrant virtualbox
$ vagrant plugin install vagrant-hostmanager --plugin-version 1.8.9
```

## Install Ansible

```sh
$ virtualenv -p python3 pyenv
$ source pyenv/bin/activate
$ pip install -r requirements.txt
```

## Install Ansible Galaxy Roles

Use [Ansible-Galaxy](https://github.com/harobed/ansible-role-sentry) to install this roles:

- [harobed.sentry](https://github.com/harobed/ansible-role-sentry)
- [harobed.nginx-proxy](https://github.com/harobed/ansible-role-nginx-proxy)

```sh
$ ansible-galaxy install -r roles/requirements.yml
- harobed.sentry (master) was installed successfully
- harobed.nginx-proxy (master) was installed successfully
```

## Start Vagrant host

```sh
$ vagrant up
```

Check that Ansible can ping `myserver` host:

```sh
$ ansible -m ping all
myserver | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

## Install Sentry

```sh
$ ansible-playbook playbooks/site.yml
```

Go to http://sentry.example.com

Default login are:

- username: admin@example.com
- password: password


## Uninstall Sentry

```sh
$ ansible-playbook playbooks/site.yml --tags sentry --extra-vars "sentry_uninstall=true"
```


## Ansible Linter checking

```sh
$ ansible-lint -v playbooks/site.yml
```
