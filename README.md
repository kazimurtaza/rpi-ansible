# Raspberry Pi Ansible

Originally by Glenn K. Lockwood, October 2018 - forked June 2020

## Introduction

This is an Ansible configuration that configures a fresh Raspbian installation
on Raspberry Pi. It is intended to be run in SSH (push) mode, where ansible
is running on the different machine, configuring multiple Raspberry Pi's simultaneously.

## Bootstrapping on Raspbian

You will need ansible installed on the host machine. This
playbook relies on Ansible 2.8 or newer, which means you can no longer use
`sudo apt-get install ansible`.  Instead, you must

    $ sudo pip install ansible

## Configuration

The `macaddrs` structure in _roles/common/vars/main.yml_ maps the MAC address of
a Raspberry Pi to its intended configuration state.  Add your Raspberry Pi's MAC
address to that structure and set its configuration accordingly.

## Running the playbook

Then run the playbook:

    $ sudo ansible-playbook local.yml 

The playbook will self-discover its settings, then idempotently configure the
Raspberry Pi.

## After running the playbook

This playbook purposely requires a few manual steps _after_ running the playbook
to ensure that it does not lock you out of your Raspberry Pi.

1. While logged in as pi, `sudo passwd glock` (or whatever username you created)
   to set a password for that user.  This is _not_ required to log in as that
   user, but it _is_ required to `sudo` as that user.  You may also choose to
   set a password for the pi and/or root users.

2. `usermod --lock pi` to ensure that the default user is completely disabled.

## Acknowledgment

I stole a lot of knowledge from https://github.com/giuaig/ansible-raspi-config/.
