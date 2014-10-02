ansible-known_hosts
===================

Add or remove a host from the known_hosts file using ansible.

This is especially useful for a new machine where you want to do something like use the 'git' module with ssh. If you don't prime the known_hosts file, ansible will hang because it is waiting for input you can't give it.

How To Use
==========

Copy the `known_hosts` bash script into a library folder adjacent to your ansible playbook. You can then define a task like this:

```
---
- hosts: myhosts
  user: deploy
  tasks:
    - name: Ensure github is in the known_hosts file
      known_hosts: host=github.com state=present
```

host
----

Required. The host to add or remove. Will also look up the IP address and add that as well.

port
----

The ssh port. Defaults to 22

file
----

The known_hosts file to append/remove the keys from. Defaults to $HOME/.ssh/known_hosts

state
-----

'present' to add the host, 'absent' to remove it. Defaults to 'present'

owner
-----

Username of the owner of 'known_hosts' file, usually useful in case you specified custom filepath in 'file' attribute.

NOTE
====

Python is considered good form for Ansible modules, but for now it was much easier to convert something I already had written in bash. It does the job, but I may some day convert it to Python in order to submit it to ansible.cc

LICENSE
=======

MIT -- See LICENSE file.
