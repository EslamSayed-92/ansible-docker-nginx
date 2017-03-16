docker-nginx
======================
[![Build Status](https://travis-ci.org/matic-insurance/ansible-nginx-container.svg?branch=master)](https://travis-ci.org/matic-insurance/ansible-nginx-container)

Role used to download, configure and run nginx-alpine container

Requirements
------------

Ubuntu 14.04 is tested.

This role uses Ansible's docker module, so requirements are [the same](https://docs.ansible.com/ansible/docker_image_module.html#requirements-on-host-that-executes-module).

Role Variables
--------------

Here is the list of Required variables with default values:
```yaml
nginx_hosts:
  - name:                        <- name of the host configuration
    https: yes/no                <- whether nginx should handle SSL
    ssl_certificate_bundle: path <- path to SSL certificate bundle,
                                    only if https is yes
    ssl_certificate_key: path    <- path to SSL certificate key,
                                    only if https is yes
    configuration_file: path     <- path to nginx configuration file
```
These variables are optional and can be changed if needed
```yaml
# Default source files location on local machine
nginx_files_local_folder: './files'

#Name of the container when it's running
nginx_container_name: nginx

#Settings path where rendered nginx files will be located
nginx_settings_path: '{{ ansible_user_dir }}/{{ nginx_container_name }}'

#Container memory limit
container_memory_limit: 256m

# Docker repository image and tag
nginx_docker_image: nginx
nginx_docker_image_tag: 1-alpine
```

Dependencies
------------

No dependencies

Example Playbook
----------------

Simpliest playbook can be following:

```yaml
- hosts: webservers
  roles:
    - role: nginx-container
      nginx_files_local_folder: './files/nginx'
      nginx_configuration_files: ['default.conf']
```

This playbook will run nginx container with name `nginx` on webserver hosts 
and will render default.conf.j2 file from `./files/ngingx` into `/etc/nginx/conf.d` folder on container
container will expose only 80 port
 
Advanced playbook with certificates and multiple ports:


License
-------

MIT

Author Information
------------------

Matic is a communication platform that connects lenders and borrowers originating a new home loan. A borrower now knows where they are in the loan process and what they need to do to complete the loan.
