# plopoyop.lego

Install & configure lego (https://go-acme.github.io/lego/)

## Table of content

- [Requirements](#requirements)
- [Default Variables](#default-variables)
  - [lego_accept_tos](#lego_accept_tos)
  - [lego_base_dir](#lego_base_dir)
  - [lego_binary](#lego_binary)
  - [lego_certificates](#lego_certificates)
  - [lego_env](#lego_env)
  - [lego_hook_scripts](#lego_hook_scripts)
  - [lego_scripts_dir](#lego_scripts_dir)
  - [lego_staging_server](#lego_staging_server)
- [Dependencies](#dependencies)
- [License](#license)
- [Author](#author)

---

## Requirements

- Minimum Ansible version: `2.10`

## Default Variables

### lego_accept_tos

Accept the Let's Encrypt Terms of Service

**_Type:_** boolean<br />

#### Default value

```YAML
lego_accept_tos: true
```

### lego_base_dir

Lego config base directory

**_Type:_** string<br />

#### Default value

```YAML
lego_base_dir: /etc/lego
```

### lego_binary

Lego binary path

**_Type:_** string<br />

#### Default value

```YAML
lego_binary: /usr/bin/lego
```

### lego_certificates

Lego certificates

**_Type:_** list<br />

#### Default value

```YAML
lego_certificates: []
```

#### Example usage

```YAML
lego_certificates:
  - domains:
      - 'example.com'
      - '*.example.com'
    email: "user@example.com"
    mode: "dns"
    dns_provider: "myprovider"
    user: root
    group: caddy
    privmode: 0640
    pubmode: 0640
    hook: "caddy-certs.sh"
    env:
      ENV_FOR_PROVIDER: "value"
  - domains:
      - 'example.com'
      - 'www.example.com'
    email: "user@example.com"
    mode: "http"
    options:
      - webroot: "/var/www/html"
    user: root
    group: www-data
    privmode: 0640
    pubmode: 0640
    staging: true
  - domains:
      - 'example.com'
      - 'www.example.com'
    email: "user@example.com"
    mode: "tls"
    options:
      - port: 443
    user: root
    privmode: 0640
    pubmode: 0640
    staging: true
```

### lego_env

Lego environment variables

**_Type:_** dict<br />

#### Default value

```YAML
lego_env: {}
```

### lego_hook_scripts

Lego hook scripts

**_Type:_** list<br />

#### Default value

```YAML
lego_hook_scripts: []
```

#### Example usage

```YAML
lego_hook_scripts:
  - name: "caddy-certs.sh"
    content: |
      #!/bin/bash
      caddy_cert_dir="/etc/ssl/caddy"
      mkdir -p "$caddy_cert_dir"
      chown -R caddy:caddy "$caddy_cert_dir"
```

### lego_scripts_dir

#### Default value

```YAML
lego_scripts_dir: '{{ lego_base_dir }}/scripts'
```

### lego_staging_server

Let's Encrypt staging server

**_Type:_** string<br />

#### Default value

```YAML
lego_staging_server: https://acme-staging-v02.api.letsencrypt.org/directory
```

## Dependencies

None.

## License

MPL-2.0

## Author

Clément Hubert
