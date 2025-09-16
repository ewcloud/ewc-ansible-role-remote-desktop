# Changelog

All notable changes to this project are documented in this file. See
[Conventional Commits](https://conventionalcommits.org) for commit guidelines.

# [1.1.0](https://github.com/ewcloud/ewc-ansible-role-remote-desktop/compare/1.0.0...1.1.0) (2025-09-16)


### Features

* Add support for RockyLinux 9.5 ([#2](https://github.com/ewcloud/ewc-ansible-role-remote-desktop/issues/2)) ([feb56eb](https://github.com/ewcloud/ewc-ansible-role-remote-desktop/commit/feb56ebf041a7798e9b7ef3fd46870b861b5aef8))

# 1.0.0 (2025-09-04)


### Bug Fixes

* Raise minimum RAM requirement for underlying VM ([8412193](https://github.com/ewcloud/ewc-ansible-role-remote-desktop/commit/8412193de01d60efa1762b641093527166151c57))
* Remove VM RAM validation to prevent false positives during role replay ([1acb8dc](https://github.com/ewcloud/ewc-ansible-role-remote-desktop/commit/1acb8dcf1620b30ec8f212d9769c9743695f1035))
* Skip installation of legacy core and default packages on RockLinux 9 ([da059b5](https://github.com/ewcloud/ewc-ansible-role-remote-desktop/commit/da059b59df52511da0eabb37091b4151a9355ea6))


### Features

* Add basic input validation ([896ddb0](https://github.com/ewcloud/ewc-ansible-role-remote-desktop/commit/896ddb057d87fcaf698c6b3b39533395b49be102))
* Allow password authentication to simplify access for LDAP-managed users ([8372acc](https://github.com/ewcloud/ewc-ansible-role-remote-desktop/commit/8372accd49d64a8a39575b3ba7d68ffa00d7d190))
* Configured Fail2ban SSH jail with user-defined IP whitelisting for brute-force protection ([f4f5bcc](https://github.com/ewcloud/ewc-ansible-role-remote-desktop/commit/f4f5bcc1fbae797f4dbc2ddffd489935a65cd48f))
* Disabled root SSH access to reduce attack surface ([3736d8a](https://github.com/ewcloud/ewc-ansible-role-remote-desktop/commit/3736d8a9d7813109870ca8cc7193e5369b6b4729))
* Downgrade supported distributions to Rocky 8 ([50a8457](https://github.com/ewcloud/ewc-ansible-role-remote-desktop/commit/50a84571ef1f7111a25bc72698183deb52ed908d))
* Enforce input type and add input validation ([2c39bdb](https://github.com/ewcloud/ewc-ansible-role-remote-desktop/commit/2c39bdb31f47645392174ab302ac6979536b79ea))
* Ensure configured services stay operational between VM reboots ([52e7d5e](https://github.com/ewcloud/ewc-ansible-role-remote-desktop/commit/52e7d5ebd1b2461f504b5faf38136900fc182341))
* Install and list versions of core requirements and optional desktop utilities ([a2eadd9](https://github.com/ewcloud/ewc-ansible-role-remote-desktop/commit/a2eadd9d4693151bea4748384f80a522ed089417))
* Linux distro check to ensure deployment on RockyLinux 8 and 9 only ([7452ac9](https://github.com/ewcloud/ewc-ansible-role-remote-desktop/commit/7452ac96f7b68b46b479577b3aee5dcb2667e172))
* Pin packages versions ([b0d9d55](https://github.com/ewcloud/ewc-ansible-role-remote-desktop/commit/b0d9d5587dcb8afe38daa63c184dfee1b21f70c6))
* Restrict supported Linux distros down to the minor version ([aca0a03](https://github.com/ewcloud/ewc-ansible-role-remote-desktop/commit/aca0a032e9b3f97dc36ac265fec02a8a2fc2c78c))
* Set input values as optional ([d274553](https://github.com/ewcloud/ewc-ansible-role-remote-desktop/commit/d27455341c38806d76050d6019cfd4f513e40629))
