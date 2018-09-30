# ansible-ssl-sync
Ansible role for SSL certificates syncing between servers through AWS S3

Create `./library` directory in your ansible project:

```
mkdir ./library
```

And configure `ansible.cfg`:

```
[defaults]
roles_path = ./library
```

Add submodule:

```
git submodule add git@github.com:kressh/ansible-ssl-sync.git library/ssl-sync
```

Use role:

```yaml
---
- hosts: lbservers
  remote_user: ansible
  become: true
  vars:
    ssl_sync_domains:
      - lb01.domain.io
    ssl_sync_upload: true
  roles:
    - ssl-sync

- hosts: lbservers
  remote_user: ansible
  become: true
  vars:
    ssl_sync_domains:
      - lb01.domain.io
      - lb02.domain.io
      - lb03.domain.io
      - lb04.domain.io
    ssl_sync_dir: /etc/nginx/ssl
    ssl_sync_download: true
  roles:
    - ssl-sync
```
