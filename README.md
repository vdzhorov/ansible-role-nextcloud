# ansible-role-nextcloud

Role for Nextcloud installation

### Prerequisites

* Disable SELinux
* Download the following roles: `vdzhorov.ansible_role_nginx`, `vdzhorov.ansible_role_mariadb`, `vdzhorov.ansible_role_php`, `vdzhorov.ansible_role_create-_ramdisk`

## Example playbook

```
- hosts: nextcloud
  roles:
    - 'ansible-role-update-all'
    - 'ansible-role-redis'
    - 'ansible-role-nextcloud'
```

## Example group_vars/nextcloud.yml

```
websites:
  - domain: 'cloud.example.com'
    user: 'cloud' # The folder where your document root is. In this case it will be /home/example/public_html/
    preset: 'nextcloud' # Can be either default, magento, opencart or wordpress. This signifies what preset configuration should be loaded for this website.
    ssl_enabled: yes
    ssl_crt_path: '/etc/pki/tls/certs/cloud.example.com.crt'
    ssl_key_path: '/etc/pki/tls/certs/cloud.example.com.key'
    gzip_enabled: no # Do not use default gzip, use Nexcloud's suggested gzip conf (nextcloud nginx preset template)
    expires_enabled: yes
    security_headers_enabled: yes
    mysql_username: 'cloud'
    mysql_database: 'cloud'
    mysql_password: super_strong_password
    nextcloud_admin_user: admin
    nextcloud_admin_password: admin_super_strong_password
    nextcloud_datadir: '/home/cloud/data'

php_version: 'php72w-'
php_packages:
  - '{{ php_version }}process'
  - '{{ php_version }}tidy'
  - '{{ php_version }}opcache'
  - '{{ php_version }}pdo'
  - '{{ php_version }}soap'
  - '{{ php_version }}xml'
  - '{{ php_version }}xmlrpc'
  - '{{ php_version }}intl'
  - '{{ php_version }}cli'
  - '{{ php_version }}common'
  - '{{ php_version }}mysqlnd'
  - '{{ php_version }}fpm'
  - '{{ php_version }}devel'
  - '{{ php_version }}gd'
  - '{{ php_version }}mbstring'

replication: False

php_fpm_pm: ondemand
php_fpm_max_children: 120
php_fpm_start_servers: 12
php_fpm_in_spare_servers: 6
php_fpm_max_spare_servers: 18
```

## Example inventory

```
[nextcloud]

nextcloud1 ansible_host=192.168.10.1
```

## Built With

* [Ansible 2.8](https://docs.ansible.com/ansible/2.8/index.html)

## Authors

* **Valentin Dzhorov** - *Initial work* - [vdzhorov](https://github.com/vdzhorov)

## Company

* **Delta.BG**

## License

This project is licensed under the MIT License.
