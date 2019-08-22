base
====

A simple ansible role to deploy our basic packages and settings.

Requirements
------------


Default Role Variables
----------------------

```

# The Debian mirror which is used in the sources.list file
base_debian_mirror: http://deb.debian.org/debian
# If the Debian distribution is not jessie, 'backports' are enabled by default
base_enable_backports: True

```

Dependencies
------------

None.

Example Playbook
----------------

For this example we will assume you have defined a host group *site* in the inventory file `hosts`.

`site-base.yml`:


```yaml
---

- hosts: site
  roles:
     - { role: jkirk.base }
```

To run this playbook you would do `ansible-playbook -i hosts site.yml`

License
-------

MIT

Author Information
------------------

Darshaka Pathirana - https://synpro.solutions
