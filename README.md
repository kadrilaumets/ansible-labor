# Ansible Role: Nginx

Paigaldab ja seadistab Nginx veebiserveri. Toetab mitut keskkonda (dev, staging, prod).

## Nõuded

- Ansible 2.9+
- Ubuntu 20.04/22.04/24.04
- Vault muutujad (kui kasutatakse HTTP auth)

## Rolli Muutujad

### Kohustuslikud (määra playbook'is)

- `environment`: "development" | "staging" | "production"
- `server_name`: "example.com"
- `site_color`: "#RRGGBB" (hex color)

### Valikulised (on defaults)

- `nginx_workers`: 2 (default: CPU arv)
- `nginx_port`: 80
- `nginx_root`: "/var/www/html"
- `debug_mode`: false
- `max_connections`: 100

### Vault muutujad (HTTP auth jaoks)

- `vault_admin_user`: "admin"
- `vault_admin_password`: "secret"

## Näited

### Development

\`\`\`yaml
- hosts: dev_servers
  roles:
    - role: nginx
      vars:
        environment: "development"
        server_name: "dev.example.local"
        debug_mode: true
        site_color: "#FFA500"
\`\`\`

### Production

\`\`\`yaml
- hosts: prod_servers
  roles:
    - role: nginx
      vars:
        environment: "production"
        server_name: "example.com"
        debug_mode: false
        site_color: "#00AA00"
        max_connections: 1000
\`\`\`

## Kasutamine

\`\`\`bash
ansible-playbook -i inventory site.yml --vault-password-file .vault_pass
\`\`\`

## Testimine

\`\`\`bash
# Idempotentsus
ansible-playbook site.yml
ansible-playbook site.yml  # changed=0

# Kontrolli
curl http://server_name
\`\`\`

## Autor

Kadri
\`\`\`
Role Name
=========

A brief description of the role goes here.

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
