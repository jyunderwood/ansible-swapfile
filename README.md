# Ansible Swapfile

Creates a swapfile on systems that don't have one.

## Usage

Requires `sudo` or root access. Includes it's own conditional checking, just include the role in your playbook. It will skip all the steps if there is already a swapfile.

```yaml
  hosts: "{{ hosts }}"
  sudo: yes

  roles:
    - jyunderwood.swapfile
```

## Variables

`swapfile_location` defaults to "/swapfile". If you want to have it created somewhere else, change this variable.

`swapfile_size` defaults to "256MB". Can be in KB, MB, or GB.

`swapfile_swappiness` defaults to "1" so the system will swap only to avoid an out-of-memory condition (kernel 3.5+). If you run a kernel older than 3.5, use "0" for the same behavior. The kernel default value is "60". Setting the value higher results in more aggressive swapping.

`swapfile_vfs_cache_pressure` defaults to "50" to reduce disk IO. The system default is "100". Decreasing this causes the kernel to prefer to retain dentry and inode caches. When set to 0, the kernel will never reclaim dentries and inodes due to memory pressure and this can easily lead to out-of-memory conditions. Increasing beyond "100" causes the kernel to prefer to reclaim dentries and inodes.

More information about `swappiness` and `vfs_cache_pressure` can be found at [kernel.org](https://www.kernel.org/doc/Documentation/sysctl/vm.txt).

## License

This Ansible role is licensed under the MIT License.

Copyright (c) 2014 Jonathan Underwood

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
