docker_owncloud
===============

This role deploys Owncloud in a Docker.
The main repo for this role is on [Le Filament GitLab](https://sources.le-filament.com/lefilament/ansible-roles/docker_owncloud.git)

Requirements
------------

None

Role Variables
--------------

Variables from default directory :
* cloud_url: URL on which Owncloud will be listening
* cloud_db_root: Database root password
* cloud_db_user: Database user
* cloud_db_pass: Database password
* cloud_admin_user: Owncloud Admin user
* cloud_admin_pass: Owncloud Admin password

* Backups (for backups to be deployed, host needs to be in maintenance_contract group)
  * swift parameters for object storage instance where backups should be pushed weekly
  * cloud_backup_pass : Passphrase for encryption of backups

Dependencies
------------

This role requires the following Ansible collection :
* community.docker

This Docker role supposes that Traefik is deployed as an inverseproxy in front of the deployed Dockers.
The following role is used by Le Filament for deploying Traefik : docker_server (https://sources.le-filament.com/lefilament/ansible-roles/docker_server)

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: docker_owncloud }
      vars:
         - { cloud_url: "cloud.example.org" }
         - { cloud_db_root: "veryUnsecureRootPassToBeModified" }
         - { cloud_db_user: "owncloud" }
         - { cloud_db_pass: "veryUnsecurePassToBeModified" }
         - { cloud_admin_user: "admin" }
         - { cloud_admin_pass: "veryUnsecureAdminPassToBeModified" }

License
-------

AGPL-3

Author Information
------------------

Le Filament (https://le-filament.com)
