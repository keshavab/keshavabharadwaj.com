+++
comments = true
date = 2015-08-21T00:00:00Z
tags = ["ansible", "with_items", "include"]
title = "Ansible - include + with_items back in 2.0"
+++

One of the widely used(abused) feature of [Ansible](https://github.com/ansible/ansible) which was taken back in 1.6 is back in 2.0.

* **include:** statement to include a file with variable name
* **include:** statement with *with_items*

Prior to 2.0, any of these operations would always result in the following error:
{{< highlight yaml >}}
---
- include: "{{ my_var }}.yml"
{{< / highlight >}}
{{< highlight bash >}}
ERROR: file not found: /path/to/ansible/provision/{{my_var}}.yml
{{< / highlight >}}

{{< highlight yaml >}}
---
- include: "{{ item }}"
  with_items:
  - "{{ my_var }}.yml"
{{< / highlight >}}
{{< highlight bash >}}
ERROR: [DEPRECATED]: include + with_items is a removed deprecated feature. Please update your playbooks.
{{< / highlight >}}


With 2.0([currently devel branch](http://docs.ansible.com/ansible/intro_installation.html#running-from-source)), these are possible now:

**include:** statement to include a file with variable name
{{< highlight yaml >}}
---
- hosts: all
  tasks:
  - include: "{{ my_var }}.yml"
{{< / highlight >}}

**include:** statement with *with_items*
{{< highlight yaml >}}
---
- hosts: all
  tasks:
  - include: play.yml {{ item }}
  with_items:
  - var_1
  - var_2
  - var_3
{{< / highlight >}}

This would help in dynamically including a file based on a variable or a fact. This would also help to iterate over the same
play/file with different values.
