# biridin
<!--
> Billie Jean is not my lover - Jackson, Michael.

> Coroi biri din!! - Channel, Joseph.
-->
## Pre conditions (Requirements?)

Install Arch Linux ARM for your version of Raspberry Pi:

- [Zero/1](https://archlinuxarm.org/platforms/armv6/raspberry-pi)

- [2B](https://archlinuxarm.org/platforms/armv7/broadcom/raspberry-pi-2)

- [3B/3B+](https://archlinuxarm.org/platforms/armv8/broadcom/raspberry-pi-3)

- [4B](https://archlinuxarm.org/platforms/armv8/broadcom/raspberry-pi-4)

Tip: Arch Linux ARM doesn't provide an `.img` file that can be "burned" to your SD card. If you have multiple Pis, assuming all sdcards are of the same size, do the process on one card and then copy it to the others.

Alert: You must do this from a Linux box (or any other OS that supports the ext4 file system in `fdisk`).

# Ansible how-to

On the host (your) machine, you'll need the latest version of Ansible and an SSH client.

On the target machine (Raspberries, hopefully), you'll need the latest version of Python, which can be installed with `pacman -S python`.

The first thing you'll need to do after booting the target machines, is build the inventory.

Find your Raspberry(ies) IP addresses using your router/network software and create the inventory file. Check `hosts.example` for an example. Tip: if possible, assign static IP addresses to your devices.

To test your inventory, you can use the command: `ansible --inventory hosts rpi4 -m ping --user alarm --ask-pass`.

This will:

- Use the inventory file named `hosts`

- Access all hosts in `rpi4` group

- Run the `ping` module on each host

- Use the `alarm` user for the SSH connection

- Ask for the `alarm` user password for SSH connection

After initial validation of the hosts file, you can start writing the playbooks for your machines.

## Intro to playbooks

Ansible playbooks are written in YAML and are run with the `ansible-playbook` command.

At the top/root level of the YAML file, you can define the groups of hosts that will be targeted by that playbook (or `all`, if you want to target all hosts in all groups of your inventory), among other options. Check the `first-playbook.yaml` for an example.

To run your playbooks, you need to (at least) provide Ansible with the playbook name and inventory file. For example: `ansible-playbook --inventory hosts first-playbook.yaml`.

Since Arch Linux ARM doesn't have sudo and the first login must be done via SSH with passwords, the full command to run the sample playbook would be:

```shell
ansible-playbook --inventory hosts first-playbook.yaml --ask-pass --ask-become-pass
```

This will set up an `ansible` user with no password and the SSH key for the `channelbeta` GitHub user.
