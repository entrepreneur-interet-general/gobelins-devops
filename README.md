# Gobelins DevOps

This is a collection of [Ansible](https://docs.ansible.com/ansible/latest/index.html) playbooks for the [Gobelins](https://github.com/entrepreneur-interet-general/gobelins) and [Gobelins Datasource](https://github.com/entrepreneur-interet-general/gobelins-datasource) projets.

It handles installing the required stack (Nginx, PostgreSQL, Elasticsearch…), and deploying the application code (git pull, frontend asset compilation, database migrations…).

It is based on [Barn](https://github.com/lasselehtinen/barn) for installation of most of the Laravel stack, but also uses [geerlingguy.postgresql](https://github.com/geerlingguy/ansible-role-postgresql) and [Ansitrano](https://github.com/ansistrano/deploy) for deployment.

## Server provisionning

1. Install Ansible. See [Ansible documentation](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)

2. For testing purposes, you may provision a local Vagrant VM.

```shell
vagrant up
```

3. Setting up support for Ansible Vault. You can either be prompted for the vault password every time you run the playbook, or save it locally in a file, as so:

```shell
echo 'thepassword' > vault_password # <- replace with real password provided.
chmod 0500 vault_password
```

4. Install the required stack on your local VM provisionned with Vagrant:

```shell
ansible-playbook --vault-password-file=vault_password -i inventory/vagrant site.yml --limit=development
```

5. Or provision the staging server:

```shell
ansible-playbook --vault-password-file=vault_password -i inventory/online site.yml  --limit=staging
```

## Application deployment

…TODO…

## Adding encrypted variables

You’ll need the vault password. We use the same password for all strings in all the variable files.

```shell
ansible-vault encrypt_string 'supersecretstring' --name 'label_name'
```

### Credits

- [Ned Baldessin](mailto:ned@baldessin.fr)
- [Lasse Lehtinen](mailto:lasse.lehtinen@iki.fi) author of [Barn](https://github.com/lasselehtinen/barn)
- [Jeff Geerling](https://www.jeffgeerling.com/) author of [geerlingguy.postgresql](https://github.com/geerlingguy/ansible-role-postgresql)
- Carlos Buenosvinos author of [Ansitrano](https://github.com/ansistrano)

### License

[MIT](https://opensource.org/licenses/MIT)

Copyright © 2018 Ministère de la Culture et de la Communication
Mobilier national et manufactures des Gobelins, de Beauvais et de la Savonnerie.
