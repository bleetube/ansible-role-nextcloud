# Ansible Role: nextcloud

This Ansible Role installs a rootless [Nextcloud](https://github.com/nextcloud/docker) container using Podman. It is intended to be composed with separate roles for Podman and any database backend such as PostgreSQL or Mariadb.

## Requirements

* [containers.podman](https://github.com/containers/ansible-podman-collections)

## Dependencies

* [podman](docs/PODMAN.md)
* [mariadb](docs/DATABASE.md) (optional)
* postgresql (optional)

## Role Variables

```yaml
nextcloud_config.NEXTCLOUD_ADMIN_USER: adminotaur
nextcloud_config.NEXTCLOUD_ADMIN_PASSWORD: "{{ lookup('ansible.builtin.env', 'NEXTCLOUD_ADMIN') }}"
nextcloud_config.MYSQL_PASSWORD: "{{ lookup('ansible.builtin.env', 'NEXTCLOUD_MARIADB') }}"
```

See the role [defaults](defaults/main.yml) and the Nextcloud [environment variable documentation](https://github.com/nextcloud/docker/blob/master/README.md#auto-configuration-via-environment-variables).

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
export NEXTCLOUD_ADMIN=$(pass generate -n NEXTCLOUD_ADMIN | tail -n1)
export NEXTCLOUD_MARIADB=$(pass generate -n NEXTCLOUD_MARIADB | tail -n1)
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