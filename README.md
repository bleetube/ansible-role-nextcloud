# Ansible Role: nextcloud

This Ansible Role installs a rootless [Nextcloud](https://github.com/nextcloud/docker) container using Podman. It is intended to be composed with separate roles for Podman and any database backend such as PostgreSQL or Mariadb.

## Requirements

* [podman](docs/PODMAN.md)
* [containers.podman](https://github.com/containers/ansible-podman-collections)

## Dependencies

* [mariadb](docs/DATABASE.md) (optional)
* postgresql (optional)

## Role Variables

See the role [defaults](defaults/main.yml) and the Nextcloud [environment variable documentation](https://github.com/nextcloud/docker/blob/master/README.md#auto-configuration-via-environment-variables). For a working example, see this [homelab stack](https://github.com/bleetube/satstack).

## Example Playbook

```yaml
- hosts: nextcloud
  roles:
    - role: fauust.mariadb
      become: true
    - role: alvistack.podman
      become: true
    - role: bleetube.nextcloud
```

## Example Deployment

```bash
ansible-playbook playbooks/nextcloud.yml
```

## Backups

TODO

## Monitoring

TODO

## Resources

* [nextcloud.admin](https://github.com/nextcloud/ansible-collection-nextcloud-admin) collection

## Thanks

Based on the original role created by [Joerg Kastning](https://www.my-it-brain.de/wordpress/zu-meiner-person/). Thank you!