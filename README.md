# Description

Installs and configures Certbot (for Let's Encrypt).

# Requirements

If installing from source, Git is required. You can install Git using the `geerlingguy.git` role.

Generally, installing from source (see section `Source Installation from Git`) leads to a better experience using Certbot and Let's Encrypt, especially if you're using an older OS release.

# Configuration

Controls how Certbot is installed. Available options are 'package', 'snap', and 'source'.
```yaml
certbot_admin_email: 'admin@example.org'
certbot_auto_renew: true
certbot_auto_renew_user: 'www-data'
certbot_auto_renew_frequency: 'daily'
certbot_auto_renew_options: "--quiet --no-self-upgrade"
certbot_certs:
  - domains: 'something.example.org'
```

The email address used to agree to Let's Encrypt's TOS and subscribe to cert-related notifications. This should be customized and set to an email address that you or your organization regularly monitors.

By default, this role configures a systemd timer to run under the provided user every day. The defaults run `certbot renew` (or `certbot-auto renew`). The account used should be a non-root account.

# Standalone Certificate Generation

Services that should be stopped while `certbot` runs it's own standalone server on ports 80 and 443. Other valid values might be `apache2`, or any other serivce that might use these ports.
```yaml
certbot_create_standalone_stop_services:
  - nginx
```
These services will only be stopped the first time a new cert is generated.

# Certbot certificate auto-renewal

You can test the auto-renewal (without actually renewing the cert) with the command:
```sh
/opt/certbot/certbot renew --dry-run
```
See full documentation and options on the [Certbot website](https://certbot.eff.org/).

## License

MIT / BSD

## Author Information

This role was created in 2016 by [Jeff Geerling](https://www.jeffgeerling.com/), author of [Ansible for DevOps](https://www.ansiblefordevops.com/).
