# ansible-swap

Configure a swap file on a new Ubuntu or CentOS host.

#### Quick Start

A task in your site.yml:

```yml
- hosts: all
  remote_user: root
  gather_facts: no

  pre_tasks:
    - name: 'Install python2 Debian/Ubuntu'
      raw: apt-get -y install python-simplejson
      ignore_errors: true

  roles:
    - swap

  vars:
    # Location of swapfile
    swap_path: "/swapfile"

    # Hosts with low RAM may need to use a small bs size
    dd_bs_size_mb: 256

    # Total size for swapfile
    # Count of how many passes dd should make at bs size
    swap_count: 16

    # 0 to 100, how often swap is utilized
    # 60 is good for desktops, 10 is good for VPS
    swappiness: 10

    # How often inode info is removed from cache
    # Usually a frequent and costly lookup if not cached
    vfs_cache_pressure: 50
```
