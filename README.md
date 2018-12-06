base
====

A simple ansible role to deploy our basic packages and settings.

Requirements
------------


Role Variables
--------------


Dependencies
------------

None.

Example Playbook
----------------

For this example we will assume you have defined a host group *site* in the inventory file `hosts`.

`site.yml`:

```
---

    - hosts: site
      roles:
         - { role: jkirk.base }
```

Currently `grml-config.yml` is included in the role base which will be a separate role in the future.
To deploy the grml-config to specific users add these lines::

```
      tasks:
        - include_tasks: roles/jkirk.base/tasks/grml-config.yml username=jane_doe
        - include_tasks: roles/jkirk.base/tasks/grml-config.yml username=john_doe

```

(*Note: The users have to exist, use role user to manage the users.*)

To run this playbook you would do `ansible-playbook -i hosts site.yml`

License
-------

MIT

Author Information
------------------

Darshaka Pathirana - https://synpro.solutions
