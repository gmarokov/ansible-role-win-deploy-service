Ansible role: win_service_deploy
=========
[![Build Status](https://travis-ci.org/gmarokov/ansible-role-win-service-deploy.svg?branch=master)](https://travis-ci.org/gmarokov/ansible-role-win-service-deploy)

Ansible role for building and deploying Windows service using MSBuild and PSCP over SSH

Requirements
------------

1. Include as a build step. Required MSBuild installed and your project's code repository checkout.
2. PuTTY cli tool pscp must also be installed.
3. WinRM must be configured and running on the target host.
4. OpenSSH must be installed, enabled by default and running on the target.

Role Variables
--------------

`backups_path` - Path to the service backup. Default to `C:/Backups/Services/{service_name}`.

`win_service_path` - Full path where service has been installed. Default set to `C:/Services`.

`repo_path` - This has to be delegated to the build server where the project repo is checkout and MSBuild is available. 

`ansible_user` - User for the target server (server_ip).

`ansible_password` - Password for the target server user.

`server_ip` - Target Windows server where the service will be deployed. 

`service_name` - Service name in the project.

`config` - Build configuration. By default is Release.


Example Playbook
----------------

```
- hosts: build-server
  vars:
    backups_path: "C:/Backups/Services"
    win_service_path: "C:/Services"
    repo_path: "C:/Repo/Services"
    ansible_user: "Administrator"
    ansible_password: "your-super-user-password"
  roles:
    - role: win_service_deploy
      vars:
       service_name: "MyWindowsService"
       config: "Release"
       server_ip: "{{ groups['example-win-services-group'][0] }}"
      tags: 
       - win-services 
```

License
-------

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

