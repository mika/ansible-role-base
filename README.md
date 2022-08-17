base
====

![Lint Code Base](https://github.com/jkirk/ansible-role-base/actions/workflows/linter.yml/badge.svg)
![Ansible Molecule](https://github.com/jkirk/ansible-role-base/actions/workflows/molecule.yml/badge.svg)

A simple ansible role to deploy our basic packages and settings.

Requirements
------------

None.

Default Role Variables
----------------------

Role variables are set and documented in [`defaults/main.yml`](defaults/main.yml).

Dependencies
------------

None.

Notes on NTP
------------

Non-default / local time servers are (currently) not supported by this role.

For `systemd-timesyncd` it is `/etc/systemd/timesyncd.conf`:
```ini
[Time]
NTP=ntp1.example.com ntp2.example.com ntp3.example.com ntp4.example.com
```

For `ntp` it is `/etc/ntp.conf`:
```text
pool time.example.com iburst
```

or

```text
server time.example.com iburst
```

We use iburst by default. I think this is OK. From ntp.conf(5):

  > iburst: When the server is unreachable, send a burst of six packets instead of the usual one. The packet spacing is normally 2 s; [...]

Use server instead of pool if no round-robin DNS is involved, though.

For `chrony` it is `/etc/chrony/chrony.conf` or a `.conf` file in `/etc/chrony/chrony.d/` (if `confdir` is defined in `/etc/chrony/chrony.conf` (the default since Debian/bullseye and later)):

```text
# Set NTP server which can be used as a time source, _prefer_ this source over sources without the prefer option and start with a burst of 4-8 requests in order to make the first update of the clock sooner (iburst)
server time.example.com prefer iburst

# Allow NTP client access from local network.
# allow 192.168.7.0/24

# Allow NTP client access from localhost (i.e. for Prometheus node_exporter)
allow 127/8

# Specify the location of the Samba ntp_signd socket when it is running as a Domain Controller (DC)
# ntpsigndsocket /var/lib/samba/ntp_signd
```

Which NTP Daemon?

We should favor `chrony` over `ntp` (from [Choosing Between NTP Daemons](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html-single/system_administrators_guide#sect-Choosing_between_NTP_daemon)):

  > Chrony should be preferred for all systems except for the systems that are managed or monitored by tools that do not support chrony, or the systems that have a hardware reference clock which cannot be used with chrony.

Further reading:

* [Differences Between ntpd and chronyd](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html-single/system_administrators_guide/index#sect-differences_between_ntpd_and_chronyd)
* [Comparison of NTP implementations](https://chrony.tuxfamily.org/comparison.html)

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

Darshaka Pathirana - <https://synpro.solutions>
