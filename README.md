# Ansible Role: nextcloud

This Ansible Role installs a rootless [Nextcloud](https://github.com/nextcloud/docker) container using Podman. It is intended to be composed with separate roles for Podman, database, and web proxy.

## Requirements

* [podman](docs/PODMAN.md)
* [containers.podman](https://github.com/containers/ansible-podman-collections)

## Dependencies

* [mariadb](docs/DATABASE.md) (optional)
* [postgresql](docs/POSTGRES.md) (optional)
* [nginx_conf](docs/examples/nginx_conf.yml) (optional)

## Role Variables

See the role [defaults](defaults/main.yml) and the Nextcloud [environment variable](https://github.com/nextcloud/docker/blob/master/README.md#auto-configuration-via-environment-variables) documentation. For a working example, see this [homelab stack](https://github.com/bleetube/satstack).

## Example Playbook

```yaml
- hosts: nextcloud
  become: true
  roles:
    - role: nginxinc.nginx_core.nginx
    - role: fauust.mariadb
    - role: alvistack.podman
    - role: bleetube.redis
    - role: bleetube.nextcloud
      become: false
  tasks:
    - import_tasks: nginx_conf.yml
```

## Systemd

```
systemctl --user status container-nextcloud.service
```

## Upgrades

Configure `nextcloud_version`.

```bash
ansible-playbook playbooks/nextcloud.yml --tags nextcloud
podman exec -it -u www-data nextcloud /var/www/html/occ app:update --all
podman exec -it -u www-data nextcloud /var/www/html/occ upgrade
```

## Backups

See the [postgres example](docs/examples/postgres-backup.sh).

## Monitoring

TODO

## Resources

* [nextcloud.admin](https://github.com/nextcloud/ansible-collection-nextcloud-admin) collection
* [Apps](https://apps.nextcloud.com/)
* [Admin Manual](https://docs.nextcloud.com/server/latest/admin_manual/)
* [User Manual](https://docs.nextcloud.com/server/latest/user_manual/)


## Thanks

Based on the original role created by [Joerg Kastning](https://www.my-it-brain.de/wordpress/zu-meiner-person/). Thank you!