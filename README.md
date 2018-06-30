# Ansible-BasicAuthManager
Ansible-BasicAuthManager in an Ansible role for setting up [BasicAuthManager](https://github.com/NIXKnight/BasicAuthManager).

## **Requirements**
At the moment this role is being written for Debian based distributions e.g. Debian/Ubuntu. It may evolve to include other major distributions. The role installs `virtualenv` and `supervisor` packages. Thsi role assumes that you have NGINX installed.

## **Role Variables**
* `BAM_USER` Sets username of the application. By default this is set to `bam`.
* `BAM_HOME` Home directory for the user set in `BAM_USER`. By default its set to `/opt/bam`.
* `BAM_CODE_DIR` Directory where BasicAuthManager code will reside. By defaults its set to use a directory named `BasicAuthManager` in home directory which is defined in `BAM_HOME`.
* `BAM_VIRTUALENV_DIR` Directory where a python virtual environment for BasicAuthManager will reside. By default its set to `venv` directory in home directory as defined in `BAM_HOME`.
* `BAM_SUPERVISOR_CONFIG_PATH` Path on the server for supervisor configuration for BasicAuthManager.
* `BAM_DOMAIN_NAME` Domain/Subdomain name that will be used to setup `server_name` in NGINX server block.
* `BAM_ADMIN` Admin user of basicAuthManager. This user has rights to create or remove users.
* `BAM_ADMIN_PASSWORD` Password for Admin user.
* `BAM_HTPASSWD_FILE` Path on the server for Htpasswd file. By default its set to htpasswd in `BAM_HOME`.
* `WEBSRV_GROUP_NAME` Web server group name. This is used to set read permission for `BAM_HTPASSWD_FILE`. By default its set to `www-data`.
* `BAM_GUNICORN_IP` Bind IP address for Gunicorn. By default, its set to `127.0.0.1`.
* `BAM_GUNICORN_PORT` Bind port for Gunicorn. By default, its set to `8000`.
* `BAM_WEBSRV_PORT` Port number of the web server (NGINX). By default its set to `80`.
* `BAM_WEBSRV_SSL_ENABLE` Enable/Disable SSL in web server (NGINX) server block. By default set to `False`.
* `BAM_WEBSRV_SSL_CERT_PATH` Path on the server where SSL certificate resides.
* `BAM_WEBSRV_SSL_KEY_PATH` Path on the server where SSL certificate key resides.
* `BAM_WEBSRV_CONF_FILE` Path on the server for NGINX server block configuration. By default its set to sites-available in NGINX configuration directory.
* `BAM_WEBSRV_ENABLED_CONF_FILE` Path on the server for NGINX server block configuration. By default its set to sites-enabled in NGINX configuration directory.
* `BAM_SMTP_FROM` Used to set From mime header of outbound email.
* `BAM_SMTP_HOST` SMTP server address.
* `BAM_SMTP_TRANSPORT` SMTP transport.
* `BAM_SMTP_PORT` SMTP port.
* `BAM_SMTP_USERNAME` SMTP username.
* `BAM_SMTP_PASSWORD` SMTP password.

Note that `BAM_SMTP_*` and `BAM_WEBSRV_SSL_*_PATH` variables are empty. You must set them.

## **Dependencies**

This role assumes that you have NGINX installed. You can either use [Ansible-NGINX](https://github.com/NIXKnight/Ansible-NGINX) role or you can use any other NGINX role out there on the internet.

## **Example Playbook**

Facts gathering must be enabled.

An example of running the role is as follows:

```yaml
- hosts: server
  gather_facts: True
  roles:
    - role: Ansible-BasicAuthManager
      BAM_DOMAIN_NAME: "this.bam.local"
      BAM_ADMIN: "admin"
      BAM_ADMIN_PASSWORD: "myadminpassword"
      BAM_SMTP_FROM: "friendly@bam.local"
      BAM_SMTP_HOST: "smtp.bam.local"
      BAM_SMTP_TRANSPORT: "STARTTLS"
      BAM_SMTP_PORT: "587"
      BAM_SMTP_USERNAME: "username@bam.local"
      BAM_SMTP_PASSWORD: "mysupersecurepassword"
```

## License
This Ansible role is licensed under MIT License.

## Author
[Saad Ali](https://github.com/nixknight)
