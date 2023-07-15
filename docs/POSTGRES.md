# PostgreSQL

This variation of the [original role](https://github.com/Tronde/ansible_role_deploy_nextcloud_with_mariadb_pod) is intended to be composed with another role that sets up the database. Here is an example using [anxs.postgresql](https://github.com/ANXS/postgresql)

## Example Playbook

```yaml
  roles:
    - anxs.postgresql
```

## Example Variables

```yaml
postgresql_users:
  - name: nextcloud
    pass: "{{ lookup('ansible.builtin.env', 'wartortle_NEXTCLOUD_POSTGRES_PASSWORD') }}"
    encrypted: yes
    state: present

postgresql_databases:
  - name: nextcloud
    owner: nextcloud
    state: present
```

In this example, there are two users because both `localhost` and `%` (all-hosts wildcard) are [mutually exclusive](https://stackoverflow.com/q/10823854/9290). I am also using environment variables to  separate secret stores from the repository.

## PG 15

I'm temporarily using this branch to get PG15:

```yaml
# - src: https://github.com/ANXS/postgresql
  - src: https://github.com/VladDm93/postgresql
    version: postgres-14-15-support
    name: anxs.postgresql
```