Caddy webserver role for Amazon Linux 2
=========

Installing PostgreSQL 14 on Amazon Linux 2 wasn't so straight forward as I had hoped for. To make it easier for other people I made this role which:

- Installs epel using amazon-linux-extras
- Adds postgres repo to yum
- Installs postgres
- Runs postgres' initdb
- Starts ands enables the postgres service
- Optionally changes the `postgres` user's password
- Optionally allows remote connections

When you allow remote connections, you can connect to your postgres database using the 'postgres' user and your specified password (or the default: 'postgres').

If you need more customisability, copy and adjust the source code.

Requirements
------------

**Python needs to be installed on the target system with `sudo yum install -y python3`. A specific version of Python (for ex `python3.8`) will not work.**


Installation
--------------

```shell
ansible-galaxy install driescruyskens.postgresql_14_amazon_linux_2
```


Role Variables and their defaults
--------------

```yaml
# Changes the postgres user's password if set. Highly recommended when allowing remote connections.
- postgres_password: "postgres"
# Enables remote connection from anywhere by anyone. (Provided credentials are correct)
- allow_remote_connections: no
```

Example Playbook
----------------

```yaml
- become: yes
  hosts: all
  name: Install PostgreSQL 14 on Amazon Linux 2
  roles: 
    - role: driescruyskens.postgresql_14_amazon_linux_2
      vars:
        - postgres_password: "{{ SECURE_PASSWORD }}"
        - allow_remote_connections: yes
```


Dependencies
------------

/


License
-------

MIT
