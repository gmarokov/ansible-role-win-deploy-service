Ansible role: win_service_deploy
=========
[![Build Status](https://travis-ci.org/gmarokov/ansible-role-win-service-deploy.svg?branch=master)](https://travis-ci.org/gmarokov/ansible-role-win-service-deploy)

Ansible role for building and deploying Windows service using MSBuild and PSCP over SSH

Requirements
------------

1. Windows build server with MSBuild installed and your project's code repository checkout
2. WinRM must be configured and running 
2. SSHD must be installed and running as a service

Role Variables
--------------

`backups_path` - Path where the service will be backup. Default to `C:/Backups/Services/{service_name}.

`server_ip` - Target Windows server where the service will be deployed. 

`service_name` - Service name, display name from the Windows service settings.

`win_service_path` - Full path where service has been installed. Default set to `C:/Services`.

`repo_path` - This has to be delegated to the build server where the project repo is checkout and MSBuild is available. 

`config` - Build configuration. By default is Release.

`ansible_user` - User for the target server (server_ip).

`ansible_password` - Password for the target server user.


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:
```
- hosts: build-server
  vars:
    backups_path: "C:/Backups/Services"
    win_service_path: "C:/Services"
    repo_path: "C:/repository"
    ansible_user: "Administrator"
    ansible_password: "you-super-user-password"
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

