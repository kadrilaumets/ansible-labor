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

