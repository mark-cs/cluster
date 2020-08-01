# Cluster Automation

## Introduction

This repository contains the automation scripts for my k3s cluster.
It uses [Ansible](https://www.ansible.com).

## Install with Ansible

Ensure that Ansible is installed.

```bash
brew install ansible
```

To run the Ansible scripts you must have must have enabled password-less SSH for each host using:
```bash
ssh-copy-id pi@host
```

The Ansible scripts can then be run:

```bash
ansible-playbook -i inventory/cluster/hosts.ini k3s.yaml
```

This will produce a running k3s cluster with Traefik and cert-manager.

## Create CA Certificate

See [ca/README.md](ca/README.md) for details.

## Configure k3s and cert-manager with the CA Certificate

Add `ca_crt` and `ca_key` variables to the Ansible variables.
The values should be the base64 encoded versions of the `ca.pem` and `ca-key.pem` files from the output of the previous step.
They can be converted to base64 by running:

```bash
cat ca/ca.pem | base64
cat ca/ca-key.pem | base64
```

