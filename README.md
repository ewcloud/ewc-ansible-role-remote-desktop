# Remote Desktop Ansible Role 

This repository contains a configuration template 
(i.e. an [Ansible Role](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html)) 
to customize your environment in the
[European Weather Cloud (EWC)](https://europeanweather.cloud/).
The template is designed to:
* Configure a pre-existing RockyLinux 8.10 virtual machine, with a minimum
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
| whitelist_ip_ranges | IP ranges (in CIDR format) to be whitelisted in Fail2ban configuration. When in doubt, do not set. Example: `['10.0.0.0/24']` | `list(string)` | n/a | no |

## SW Bill of Materials (SBoM)
Third-party components used in the resulting environment.

### RockyLinux 8.10 Environment
The following components will be included in the resulting environment:

| Component | Version | License | Home URL |
|------|---------|---------|--------------|
| x2goserver | 4.1 | GPLv2+ | http://www.x2go.org |
| x2goserver-xsession | 4.1 | GPLv2+ | http://www.x2go.org |
| caja | 1.26 | GPLv2+ | http://mate-desktop.org |
| dconf | 0.28 | LGPLv2+ | http://live.gnome.org/dconf |
| gtk2-engines | 2.20 | LGPLv2+ | http://download.gnome.org/sources/gtk-engines |
| gvfs | 1.36 | GPLv3 | https://wiki.gnome.org/Projects/gvfs |
| gvfs-fuse | 1.36 | GPLv3 | https://wiki.gnome.org/Projects/gvfs |
| gvfs-gphoto2 | 1.36 | GPLv3 | https://wiki.gnome.org/Projects/gvfs |
| gvfs-mtp | 1.36 | GPLv3 | https://wiki.gnome.org/Projects/gvfs |
| gvfs-smb | 1.36 | GPLv3 | https://wiki.gnome.org/Projects/gvfs |
| libmatekbd | 1.26 | LGPLv2+ | http://mate-desktop.org |
| libmateweather | 1.26 | GPLv2+ | http://mate-desktop.org |
| libsecret | 0.18 | LGPLv2+ | https://wiki.gnome.org/Projects/Libsecret |
| marco | 1.26 | GPLv2+ | http://mate-desktop.org |
| mate-backgrounds | 1.26 | GPLv2+ | http://mate-desktop.org |
| mate-control-center | 1.26 | GPLv2+ | http://mate-desktop.org |
| mate-desktop | 1.26 | GPLv2+ | http://mate-desktop.org |
| mate-desktop-libs | 1.26 | GPLv2+ | http://mate-desktop.org |
| mate-icon-theme | 1.26 | GPLv2+ | http://mate-desktop.org |
| mate-media | 1.26 | GPLv2+ | http://mate-desktop.org |
| mate-menus | 1.26 | GPLv2+ | http://mate-desktop.org |
| mate-notification-daemon | 1.26 | GPLv2+ | http://mate-desktop.org |
| mate-panel | 1.26 | GPLv2+ | http://mate-desktop.org |
| mate-polkit | 1.26 | GPLv2+ | http://mate-desktop.org |
| mate-power-manager | 1.26 | GPLv2+ | http://mate-desktop.org |
| mate-session-manager | 1.26 | GPLv2+ | http://mate-desktop.org |
| mate-settings-daemon | 1.26 | GPLv2+ | http://mate-desktop.org |
| mate-system-monitor | 1.26 | GPLv2+ | http://mate-desktop.org |
| mate-themes | 3.22 | GPLv2+ | http://mate-desktop.org |
| xdg-user-dirs-gtk | 0.10 | GPL+ | http://freedesktop.org/wiki/Software/xdg-user-dirs |
| yelp | 3.28 | LGPLv2+ | https://wiki.gnome.org/Apps/Yelp |
| NetworkManager | 1.40 | GPLv2+ | https://networkmanager.dev/ |
| NetworkManager-l2tp | 1.20 | GPLv2+ | https://github.com/nm-l2tp/NetworkManager-l2tp |
| NetworkManager-openconnect | 1.2 | GPLv2+ | http://www.gnome.org/projects/NetworkManager |
| NetworkManager-openvpn | 1.8 | GPLv2+ |	http://www.gnome.org/projects/NetworkManager |
| NetworkManager-pptp | 1.2 | GPLv2+ | http://www.gnome.org/projects/NetworkManager |
| brasero | 3.12 | GPLv3+ | https://wiki.gnome.org/Apps/Brasero |
| caja-image-converter | 1.26 | GPLv2+ | http://mate-desktop.org |
| caja-open-terminal | 1.26 | GPLv2+ | http://mate-desktop.org |
| caja-sendto | 1.26 | GPLv2+ | http://mate-desktop.org |
| dconf-editor | 3.28 | LGPLv2+ | https://wiki.gnome.org/Projects/dconf |
| engrampa | 1.26 | GPLv2+ | http://mate-desktop.org |
| eom | 1.26 | GPLv2+ | http://mate-desktop.org |
| filezilla | 3.55 | GPLv2+ | https://filezilla-project.org |
| firefox | 128.11 | MPLv1.1 | https://www.mozilla.org/firefox |
| firewall-config | 0.9 | GPLv2+ | http://www.firewalld.org |
| gparted | 1.3 | GPLv2+ | http://gparted.org |
| gucharmap | 12.0 | GPLv3+ | https://wiki.gnome.org/Apps/Gucharmap |
| lightdm | 1.30 | GPLv3+ | https://www.freedesktop.org/wiki/Software/LightDM |
| lightdm-gtk | 2.0 | GPLv2+ | http://mate-desktop.org |
| mate-applets | 1.26 | GPLv2+ | http://mate-desktop.org |
| mate-calc | 1.24 | GPLv2+ | http://mate-desktop.org |
| mate-dictionary | 1.26 | GPLv2+ | http://mate-desktop.org |
| mate-disk-usage-analyzer | 1.26 | GPLv2+ | http://mate-desktop.org |
| mate-menus-preferences-category-menu | 1.26 | GPLv2+ | http://mate-desktop.org |
| mate-screensaver | 1.26 | GPLv2+ | http://mate-desktop.org |
| mate-screenshot | 1.26 | GPLv2+ | http://mate-desktop.org |
| mate-search-tool | 1.26 | GPLv2+ | http://mate-desktop.org |
| mate-system-log | 1.26 | GPLv2+ | http://mate-desktop.org |
| mate-terminal | 1.26 | GPLv2+ | http://mate-desktop.org |
| mozo | 1.26 | LGPLv2+ | http://mate-desktop.org |
| network-manager-applet | 1.26 | GPLv2+ | http://www.gnome.org/projects/NetworkManager |
| p7zip | 16.2 | LGPLv2 | http://p7zip.sourceforge.net |
| p7zip-plugins | 16.2 | LGPLv2+ | http://p7zip.sourceforge.net |
| pluma | 1.26 | GPLv2+ | http://mate-desktop.org |
| seahorse | 3.20 | GPLv2+ | https://github.com/darkshram/seahorse-caja |
| setroubleshoot | 3.3 | GPLv2+ | https://gitlab.com/setroubleshoot/framework |
| simple-scan | 3.36 | GPLv3+ | https://launchpad.net/simple-scan |
| totem | 3.26 | LGPLv2+ | https://wiki.gnome.org/Apps/Videos |
| transmission-gtk | 3.0 | MIT | http://www.transmissionbt.com |
| vim-enhanced | 8.0 | MIT | http://www.vim.org/ |
| caja-actions | 1.26 | GPLv2+ | https://github.com/raveit65/caja-actions |
| caja-beesu | 1.26 | GPLv2+ | http://mate-desktop.org |
| firewall-applet | 0.9 | GPLv2+ | http://www.firewalld.org |
| mate-sensors-applet | 1.26 | GPLv2+ | http://mate-desktop.org |
| mate-utils | 1.26 | GPLv2+ | http://mate-desktop.org |
| libreoffice | 6.4 | MPLv1.1 | http://www.libreoffice.org |
| firewalld | 0.9 | GPLv2+ | http://www.firewalld.org |
| fail2ban | 1.0 | GPLv2+ | http://fail2ban.sourceforge.net |
| gvfs-afc | 1.36 | GPLv3 | https://wiki.gnome.org/Projects/gvfs |
| gvfs-archive | 1.36 | GPLv3 | https://wiki.gnome.org/Projects/gvfs |
| rhythmbox | 3.4 | GPLv2+ | https://wiki.gnome.org/Apps/Rhythmbox |


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
