# Ansible Vagrant Set-Up

## What this does

Uses Ansible to create configured Vagrant folders/files with local-only SSH keys for Ansible to then provision for local development, as if they were standard remote machines.

### See an example 

Check out the **example-output** branch to see a finished playbook build.

## Prerequisites

Ansible 2.8+

Vagrant

## Instructions

- Update Vagrant configurations with your variables in `your_project/ansible/roles/vagrant-setup/defaults/main.yml`

- update the `vagrant-setup` role tasks in `your_project/ansible/roles/tasks/main.yml` with the new variable items

- `cd` into the `ansible` directory

- run `ansible-playbook setup-playbook.yml`

This will create the Vagrant folder(s), keys, and add the new inventory to Ansible.

Go back to the parent directory and into a Vagrant folder. Start Vagrant:

```
cd ../vagrant
vagrant up
```

`vagrant up` will run a short shell script to add the SSH key to the `vagrant` user. 

You can now run Ansible against the Vagrant boxes. Add any roles or tasks to `vagrant-playbook.yml`. 

You can also SSH directly into the running Vagrant box as a typical remote server with the created private key in the Ansible folder as `vagrant@<ip>` instead of running `vagrant ssh`. 

Example:

```
ssh -i ansible/vagrant_ssh/vagrant_rsa vagrant@192.168.10.30
```

## Warning

Don't save SSH keys in version control *ever*. Generate these keys strictly for local ease of use.

