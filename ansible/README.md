# Cluster Automation

## Introduction

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

This will produce a running k3s cluster.
