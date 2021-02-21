# Desktop Ansible

Ansible playbook to install my personal computer from scratch (including the partitioning and bootloader config. (uses full disk)
Initial install heavily based of: https://github.com/jsf9k/ansible-arch-install

## iso-install

Boot the host you want to manage with an arch iso. run the following commands:

1. `passwd` ("root" is used for the arch iso password, can be changed in the `hosts` file)
2. `systemctl start sshd`
3. `ip a` (to get the host ip address, change this in the inventory file)

Change the variables you want under iso-installation.yaml.
- `install_drive`: drive that will be wiped and used for installing arch. 2 partitions will be made
- `user`:
  - `name`: user to create that is not root
  - `password`: encrypted user password, can be clear text as well but this is not advised
  - `pub_key_location`: public key to add to host so we can run the common playbook after that
- `hostname`: sets hostname for networking
- `timezone`: timezone to set on the host

Run the playbook:
`ansible-playbook -i hosts iso-installation.yaml`

*remarks*:
- currently locale is hard set
- currently pacman rankmirrors is using central europe as location
- grub is set to efi

## common
this relies on ansible-aur from the following repo: https://github.com/kewlfft/ansible-aur

This should be runnable on most of the arch installs (works on arm as well). Items set in `iso-install` can be overridden for hosts that are maybe not provisioned with Ansible.

## WSL Prerequisites

Run before ansible:
- https://github.com/yuk7/ArchWSL/wiki/How-to-Setup
- pacman -S openssh
- systemctl start sshd
- systemctl enable sshd
