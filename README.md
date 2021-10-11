Packer template as Ubuntu for ARM with Prallels
==

This is Packer templates to build a Vagrant box as Ubuntu for ARM with Parallels on Apple silicon.
These are based on [chef/bento](https://github.com/chef/bento).

Requirement
--

Require these:

- [Apple Silicon Mac](https://www.apple.com/mac/)
- [Prallels Pro Edition](https://www.parallels.com/jp/products/desktop/pro/)
- [Packer](https://www.packer.io/)

Usage
--

Run this:

```sh
$ packer build ubuntu-(20|21).04-arm64.json
```
