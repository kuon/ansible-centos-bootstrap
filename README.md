CentOS Bootstrap
================

This role will bootstrap a CentOS 7 node.

It consists of two steps, the first step will copy an ssh key and disable root password login, the second step will configure the system.

Requirements
------------

A CentOS instance with root ssh access with password, an account with sudo priviledges will be created and the root user login disabled.

The role will set the hostname of the host using a DNS query, for this it is required that the inventory hostname resolves to a single ipv4 address.

Role Variables
--------------

Name of admin account:

`bootstrap_username` = `deploy`

Dependencies
------------

none

Usage
-----

1) First pass


You must first execute the playbook with the root user and the bootstrap tag, like so:

Inventory:

    [bootstrap]

    somehost.somedomain.com ansible_ssh_pass=ched3bYg8Doiv6h


Playbook:

    - hosts: bootstrap
      remote_user: root
      gather_facts: false

      roles:
      - { role: kuon.centos-bootstrap, bootstrap_operation: 'bootstrap' }


2) Second pass


Inventory:

    [somegroup]

    somehost.somedomain.com


Playbook:

    - hosts: somegroup
      remote_user: deploy
      sudo: true
      gather_facts: false

      roles:
      - { role: kuon.centos-bootstrap, bootstrap_operation: 'configure' }


License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
