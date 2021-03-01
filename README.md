# Ansible role to deploy Owncloud server docker

[![](https://img.shields.io/badge/licence-AGPL--3-blue.svg)](http://www.gnu.org/licenses/agpl "License: AGPL-3")

This role allows you to deploy Owncloud docker with associated MariaDB and Redis.

On top of deploying and starting the Owncloud instance, the following functionality has been added:
- backup and restore based on duplicity docker from [Tecnativa](https://github.com/Tecnativa/docker-duplicity) which has been customized for our needs to backup on Public Object Storage (OpenShift) directory and running it every week using cron, keeping only the last 4 weeks backups (you can modify these parameters in templates/backups.yaml.j2)

Prior to running this role, you would need to have docker installed on your server and a traefik proxy (which is the purpose of [this role](https://github.com/lefilament/ansible_role_docker_server))

In order to use this role, you would need to define the following variables for your server (in hostvars for instance) - Only the names of the variables are provided below (not the values) for these used by this role to properly configure everything, you may copy this file directly in hostvars and set the variable although we could only encourage you to use an Ansible vault and refer vault variables from there:

```json
## Ansible configuration for connecting to remote host
# IP address of server
ansible_host: 
# User to be used on server (to which Ansible server public key has been provided)
ansible_user: 
# Encryped password (for elevating rights / sudo)
ansible_become_pass: 
# Server SSHD port
ansible_port: 


## Owncloud configuration
# Owncloud URL
cloud_url: 
# Owncloud DB user/role
cloud_db_user: 
# Owncloud DB password
cloud_db_pass: 
# Owncloud MySQL root password
cloud_db_root: 
# Owncloud Admin user
cloud_admin: 
# Owncloud Admin password
cloud_admin_pass: 

# Swift Configuration
swift_cloud_username:
swift_cloud_password:
swift_cloud_authurl:
swift_cloud_authversion:
swift_cloud_tenantname:
swift_cloud_tenantid:
swift_cloud_regionname:


```

# Procedure to restore Owncloud from backup

In order to restore Owncloud database and files from backup, change directory to /home/docker/backups and run the following command:
`docker-compose -f backup-owncloud.yaml run --rm backup_owncloud sh -c "restore --force && mysql -h \$MYSQL_HOST -u \$MYSQL_USER -p\$MYSQL_PASSWORD \$MYSQL_DATABASE < \$SRC/mysql_db_\$MYSQL_DATABASE.sql"`



# Credits

## Contributors

* Remi Cazenave <remi-filament>


## Maintainer

[![](https://le-filament.com/img/logo-lefilament.png)](https://le-filament.com "Le Filament")

This role is maintained by Le Filament
