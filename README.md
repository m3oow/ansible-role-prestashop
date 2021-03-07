# Ansible Role: Prestashop 1.7.x

An Ansible Role that installs Prestashop 1.7.x on Debian / Ubuntu.

## Requirements

PrestaShop 1.7.x has the following [system requirements](https://devdocs.prestashop.com/1.7/basics/installation/system-requirements/):
* System: Unix, Linux or Windows.
* Web server: Apache Web Server 2.2, Nginx 1.0 or any later version.
* PHP: PHP 7.1 or later ([compatibility chart](https://devdocs.prestashop.com/1.7/basics/installation/system-requirements/#php-compatibility-chart)).
* MySQL: 5.6 minimum, a recent version is recommended.

I recommend using the following galaxy roles (and override their default variables to meet Prestashop requirements) :
* `geerlingguy.mysql`
* `geerlingguy.apache`
* `geerlingguy.php`

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```yml
prestashop_version: 1.7.7.2
```

Prestashop version to deploy.

```yml
prestashop_url_download: "https://download.prestashop.com/download/releases/prestashop_{{ prestashop_version }}.zip"
```

The URL from which to download Prestashop installer.

```yml
prestashop_root_path: "/var/www/prestashop"
```

Prestashop web root (to reference in your local webserver).

```yml
prestashop_user: 'www-data'
prestashop_group: 'www-data'
prestashop_chmod: '0750'
```

Prestashop user, group and chmod (must be the same user and / or group than your webserver system user and group).

```yml
prestashop_language: 'fr'
prestashop_timezone: 'Europe/Paris'
```

To set according to your region.


```yml
prestashop_domain: "prestashop.test"
```

Prestashop domain name (will be written in the database and all `.htaccess` files). If this domain has to change on a working shop, you will have to modify manually the database and `.htaccess` files.

```yml
prestashop_db_server: 'localhost'
prestashop_db_name: 'prestashop'
prestashop_db_user: 'prestashop'
prestashop_db_password: 'prestashop'
prestashop_db_clear: 1
prestashop_db_create: 1
prestashop_engine: 'InnoDB'
prestashop_prefix: 'ps_'
```

Prestashop database configuration values. Those values are passed to the PHP installation script of Prestashop (more information [here](http://doc.prestashop.com/display/PS17/Installing+PrestaShop+using+the+command-line+script)):

* `db_clear` : if set to `1`, the installation process will drop existing tables in `prestashop_db_name`.
* `db_create` : if set to `1`, `prestashop_db_name` will be created by the installation process.

```yml
prestashop_name: 'Prestashop'
prestashop_activity: 0
prestashop_country: 'fr'
prestashop_firstname: 'John'
prestashop_lastname: 'Doe'
prestashop_email: 'admin@prestashop.com'
prestashop_password: 'prestashop'
prestashop_license: 0
prestashop_newsletter: 0
prestashop_send_email: 0
prestashop_all_languages: 0
```

Other basic configuration values for your shop. Those values are passed to the PHP installation script of Prestashop (more information [here](http://doc.prestashop.com/display/PS17/Installing+PrestaShop+using+the+command-line+script).

* `prestashop_activity` : not documented by Prestashop.
* `prestashop_email` : login for the administration backend.
* `prestashop_password` : password for the administration backend.
* `prestashop_license` : set to `0`, so that Prestashop license is not displayed.
* `prestashop_newsletter` : can be set to `1` to subscribe `prestashop_email` to Prestashop's newsletter.
* `prestashop_send_email`: set to `0` so that no notifications are sent to `prestashop_email`.
* `prestashop_all_languages` : set to `0` to prevent download of all available languages for Prestashop.

```yml
prestashop_admin_folder_name: "admin"
```

Name of the Prestashop folder which hold the administration backend (for security reasons, it is highly recommended to change this value with a random name, so that directory enumeration is made difficult for a potential attacker).

## Dependencies

None.

## Example Playbook

Create or add to your roles dependency file (e.g requirements.yml):

```yml
---
- src: https://github.com/m3oow/ansible-role-prestashop
  version: master
  name: m3oow.prestashop
```

Install the role with `ansible-galaxy` command:

```yml
ansible-galaxy install -r requirements.yml
```

Use in a playbook:

```yml
---
- hosts: someserver
  roles:
    - m3oow.prestashop

## License

MIT / BSD

## Author Information

This role was created in 2021 by [m3oow](https://github.com/m3oow/).
