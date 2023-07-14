# Mariadb

This variation of the [original role](https://github.com/Tronde/ansible_role_deploy_nextcloud_with_mariadb_pod) is intended to be composed with another role that sets up the database. Here is an example using [fauust.mariadb](https://github.com/fauust/ansible-role-mariadb)

## Example Playbook

```yaml
  roles:
    - fauust.mariadb
```

## Example Variables

```yaml
mariadb_databases:
  - name: nextcloud
    collation: utf8_general_ci
    encoding: utf8
    replicate: false

mariadb_users:
  - name: nextcloud
    host: localhost
    password: "{{ lookup('ansible.builtin.env', 'NEXTCLOUD_MARIADB') }}"
    priv: "nextcloud.*:ALL"
    state: present
  - name: nextcloud
    host: '%'
    password: "{{ lookup('ansible.builtin.env', 'NEXTCLOUD_MARIADB') }}"
    priv: "nextcloud.*:ALL"
    state: present
```
In this example, there are two users because both `localhost` and `%` (all-hosts wildcard) are [mutually exclusive](https://stackoverflow.com/q/10823854/9290). I am also using environment variables to  separate secret stores from the repository.