# Remote Desktop Ansible Role 

This repository contains a configuration template 
(i.e. an [Ansible Role](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html)) 
to customize your environment in the
[European Weather Cloud (EWC)](https://europeanweather.cloud/).
The template is designed to:
* Configure a pre-existing virtual machine running RockyLinux version 9 or 8, with a minimum
  recommended 4GB of RAM, such that it:
  * Enables users to operate the remote hosts through a graphical desktop 
  (i.e. a [MATE desktop environment](https://mate-desktop.org/)), over a low or high bandwidth connection.

## Copyright and License
Copyright © EUMETSAT 2025.

The provided code and instructions are licensed under the [MIT license](./LICENSE).
They are intended to automate the setup of an environment that includes 
third-party software components.
The usage and distribution terms of the resulting environment are 
subject to the individual licenses of those third-party libraries.

Users are responsible for reviewing and complying with the licenses of
all third-party components included in the environment.

Contact [EUMETSAT](http://www.eumetsat.int) for details on the usage and distribution terms.

## Usage

The step-by-step described below assume your local file system follows the 
example structure below, with `ewc-ansible-role-remote-desktop` being a clone of this
repository:
```
.
├── roles
│   └── ewc-ansible-role-remote-desktop
├── inventory.yml
└── playbook.yml
```

### 1. Specify the target host and SSH credentials
Create an inventory file to specify address/credentials that Ansible should use
to reach the virtual machine you wish to configure:
```yaml
# inventory.yml
---
ewcloud:
  hosts:
    remote_desktop:
      ansible_python_interpreter: /usr/bin/python3
      ansible_host: <add the IPV4 address of the target host>
      ansible_ssh_private_key_file: <add the path to local SSH RSA private key file>
      ansible_user: <add the username which owns the SSH RSA private key >
```
### 2. Customize the template

Edit input values for the template [variables](./vars/main.yml) as needed (see
[Inputs](#inputs) section for details).
Then, proceed to create an Ansible Playbook file to load your customizations: 

```yaml
# playbook.yml
---
- name: Configure X2Go Server on RockyLinux
  hosts: remote_desktop
  become: true
  become_user: root
  become_method: ansible.builtin.sudo

  roles:
    - ewc-ansible-role-remote-desktop
```

### 3. Apply the template


You can apply changes on the target host by running:
```bash
ansible-playbook -i inventory.yml playbook.yml
```

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|----------|
| fail2ban_whitelist_ip_ranges | IP ranges (in CIDR format) to be whitelisted in Fail2ban configuration. When in doubt, set as an empty string. Examples: `''`, `['10.0.0.0/24']` | `list(string)` | n/a | yes |

## Dependencies
> 💡 Upon execution, a SBOM (SPDX format) is auto-generated and stored in the VM's file system root directory (see `/sbom.json`).

The following third-party components will be included in the resulting environment:

| Component | Home URL |
|------|---------|
 | x2goserver | http://www.x2go.org |
 | x2goserver-xsession | http://www.x2go.org |
 | caja | http://mate-desktop.org |
 | dconf | http://live.gnome.org/dconf |
 | gtk2-engines | http://download.gnome.org/sources/gtk-engines |
 | gvfs | https://wiki.gnome.org/Projects/gvfs |
 | gvfs-fuse | https://wiki.gnome.org/Projects/gvfs |
 | gvfs-gphoto2 | https://wiki.gnome.org/Projects/gvfs |
 | gvfs-mtp | https://wiki.gnome.org/Projects/gvfs |
 | gvfs-smb | https://wiki.gnome.org/Projects/gvfs |
 | libmatekbd | http://mate-desktop.org |
 | libmateweather | http://mate-desktop.org |
 | libsecret | https://wiki.gnome.org/Projects/Libsecret |
 | marco | http://mate-desktop.org |
 | mate-backgrounds | http://mate-desktop.org |
 | mate-control-center | http://mate-desktop.org |
 | mate-desktop | http://mate-desktop.org |
 | mate-desktop-libs | http://mate-desktop.org |
 | mate-icon-theme | http://mate-desktop.org |
 | mate-media | http://mate-desktop.org |
 | mate-menus | http://mate-desktop.org |
 | mate-notification-daemon | http://mate-desktop.org |
 | mate-panel | http://mate-desktop.org |
 | mate-polkit | http://mate-desktop.org |
 | mate-power-manager | http://mate-desktop.org |
 | mate-session-manager | http://mate-desktop.org |
 | mate-settings-daemon | http://mate-desktop.org |
 | mate-system-monitor | http://mate-desktop.org |
 | mate-themes | http://mate-desktop.org |
 | xdg-user-dirs-gtk | http://freedesktop.org/wiki/Software/xdg-user-dirs |
 | yelp | https://wiki.gnome.org/Apps/Yelp |
 | NetworkManager | https://networkmanager.dev |
 | NetworkManager-l2tp | https://github.com/nm-l2tp/NetworkManager-l2tp |
 | NetworkManager-openconnect | http://www.gnome.org/projects/NetworkManager |
 | NetworkManager-openvpn | http://www.gnome.org/projects/NetworkManager |
 | NetworkManager-pptp | http://www.gnome.org/projects/NetworkManager |
 | brasero | https://wiki.gnome.org/Apps/Brasero |
 | caja-image-converter | http://mate-desktop.org |
 | caja-open-terminal | http://mate-desktop.org |
 | caja-sendto | http://mate-desktop.org |
 | dconf-editor | https://wiki.gnome.org/Projects/dconf |
 | engrampa | http://mate-desktop.org |
 | eom | http://mate-desktop.org |
 | filezilla | https://filezilla-project.org |
 | firefox | https://www.mozilla.org/firefox |
 | firewall-config | http://www.firewalld.org |
 | gparted | http://gparted.org |
 | gucharmap | https://wiki.gnome.org/Apps/Gucharmap |
 | lightdm | https://www.freedesktop.org/wiki/Software/LightDM |
 | lightdm-gtk | http://mate-desktop.org |
 | mate-applets | http://mate-desktop.org |
 | mate-calc | http://mate-desktop.org |
 | mate-dictionary | http://mate-desktop.org |
 | mate-disk-usage-analyzer | http://mate-desktop.org |
 | mate-menus-preferences-category-menu | http://mate-desktop.org |
 | mate-screensaver | http://mate-desktop.org |
 | mate-screenshot | http://mate-desktop.org |
 | mate-search-tool | http://mate-desktop.org |
 | mate-system-log | http://mate-desktop.org |
 | mate-terminal | http://mate-desktop.org |
 | mozo | http://mate-desktop.org |
 | network-manager-applet | http://www.gnome.org/projects/NetworkManager |
 | p7zip | http://p7zip.sourceforge.net |
 | p7zip-plugins | http://p7zip.sourceforge.net |
 | pluma | http://mate-desktop.org |
 | seahorse | https://github.com/darkshram/seahorse-caja |
 | setroubleshoot | https://gitlab.com/setroubleshoot/framework |
 | simple-scan | https://launchpad.net/simple-scan |
 | totem | https://wiki.gnome.org/Apps/Videos |
 | transmission-gtk | http://www.transmissionbt.com |
 | vim-enhanced | http://www.vim.org/ |
 | caja-actions | https://github.com/raveit65/caja-actions |
 | caja-beesu | http://mate-desktop.org |
 | firewall-applet | http://www.firewalld.org |
 | mate-sensors-applet | http://mate-desktop.org |
 | mate-utils | http://mate-desktop.org |
 | libreoffice | http://www.libreoffice.org |
 | firewalld | http://www.firewalld.org |
 | fail2ban | http://fail2ban.sourceforge.net |
 | gvfs-afc (RockyLinux 8 only) | https://wiki.gnome.org/Projects/gvfs |
 | gvfs-archive (RockyLinux 8 only)| https://wiki.gnome.org/Projects/gvfs |
 | rhythmbox (RockyLinux 8 only)| https://wiki.gnome.org/Apps/Rhythmbox |


## Changelog
All notable changes (i.e. fixes, features and breaking changes) are documented 
in the [CHANGELOG.md](./CHANGELOG.md).

## Contributing

Thanks for taking the time to join our community and start contributing!
Please make sure to:
* Familiarize yourself with our [Code of Conduct](./CODE_OF_CONDUCT.md) before 
contributing.
* See [CONTRIBUTING.md](./CONTRIBUTING.md) for instructions on how to request 
or submit changes.

## Authors

[European Weather Cloud](http://support.europeanweather.cloud/) 
<[support@europeanweather.cloud](mailto:support@europeanweather.cloud)>
