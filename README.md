Ansible Role: Debpkg
=========

Install and set environments for building Debian packages with sbuild.

Requirements
------------

Debian-based distribution who have sbuild(=> 0.71) installed or available from the package management tool, apt.

Role Variables
--------------

### `debpkg_chroots`

By default this dictionary is empty.

Chroot that will be created by sbuild-createchroot if not present.

Theses keys can be used to set options to the sbuild-createchroot command.

##### `suite`

Default: dictionary item.key. Set the Debian-based codenmae distribution, ex: jessie.

##### `prefix`

Default: dictionary item.key. Set the chroot prefix name, ex: jessie-backports.

##### `arch`

Default: 'amd64'. Set the processor architecture wanted for the chroot, ex: 'i386'.

##### `suffix`

Default: 'sbuild'. Set the suffix chroot name, ex: test.

##### `extra_repository`

Default: ''. Add an extra apt source list, ex: 'deb http://deb.debian.org/debian jessie-backports main'.

##### `homedir`

Default: 'debpkg\_schroot\_homedir/item.key', debpkg\_schroot\_homedir is a distribution specific variable set into vars/{{ ansible\_distribution }}.yml file. Set the full path of the chroot, ex: /home/sbuild/jessie.

##### `mirror`

Default: 'debpkg\_schroot\_mirror', another distribution specific variable. Set the packages archive mirror used, ex: 'http://debian.mirror.test.org/debian/'.

Dependencies
------------

None.

Example Playbook
----------------

```yaml
- hosts: servers
  become: yes
  roles:
  - maxlareo.debpkg
  vars:
  - debpkg_chroots:
      wheezy:
      jessie:
      jessie-backports:
        suite: jessie
        prefix: jessie-backports
        extra_repository: 'deb http://deb.debian.org/debian jessie-backports main'
      xenial-test:
        suite: xenial
        prefix: whatever
        suffix: iwant
        arch: i386
        homedir: '/home/sbuild-test/xenial-testing-var'
        mirror: 'http://archive.ubuntu.com/ubuntu'
```

Exemple made on Debian distribution !

On other distributions the default mirror variable will not be the same, so for Debian chroot the mirror variable is optional for a Debian host, but for an Ubuntu host, by exemple, it will be mandatory on a Debian host !

License
-------

Apache-2.0

Author Information
------------------

Created by [Maxime Lareo](https://github.com/maxlareo).
