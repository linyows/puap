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

Note
--

Parallels tools from the parallels tools installer attached with packer will fail to install.
Therefore, it is necessary to set the option not to clean up the packer and complete the following work manually.

```sh
$ packer -on-error = abort --only = parallels-iso build ubuntu-(20 | 21) .04-arm64.json
...
    parallels-iso: Error during report about failed installation of parallels tools.
    parallels-iso: Error: failed to install Parallels Guest Tools!
==> parallels-iso: Script exited with non-zero exit status: 167.Allowed exit codes are: [0]
```

After installing Parallels tools from the GUI,
login with `user: vagrant, pw: vagrant` on the console and complete the image creation with the following command.

```sh
# sudo mount /dev/dvd /tmp/mnt && cd /tmp/mnt && sudo ./install
# sudo umount /tmp/arallels && sudo umount /tmp/mnt
# cd /tmp
# wget https://raw.githubusercontent.com/linyows/ptuap/main/scripts/cleanup.sh && chmod +x cleanup.sh && sudo ./cleanup.sh
# wget https://raw.githubusercontent.com/linyows/ptuap/main/scripts/minimize.sh && chmod +x minimize.sh && sudo PACKER_BUILDER_TYPE=parallels-iso ./minimize.sh
# rm minimize.sh
# sudo su
# echo -e '#!/bin/sh\n'\
'# Shared folders auto-mount is disabled by Vagrant ' \
> "/usr/bin/prlfsmountd"
# exit
# exit
```

```sh
$ tree builds/packer-ubuntu-(20|21).04-arm64-parallels/
packer-ubuntu-21.04-arm64-parallels/
├── Vagrantfile
├── metadata.json
└── ubuntu-21.04-arm64.pvm
    ├── NVRAM.dat
    ├── VmInfo.pvi
    ├── config.pvs
    └── harddisk1.hdd
        ├── DiskDescriptor.xml
        ├── harddisk1.hdd
        ├── harddisk1.hdd.0.{5fbaabe3-6958-40ff-92a7-860e329aab41}.hds
        └── harddisk1.hdd.drh
$ cd builds/packer-ubuntu-(20|21).04-arm64-parallels
$ cat << EOL > Vagrantfile

# The contents below were provided by the Packer Vagrant post-processor


# The contents below (if any) are custom contents provided by the
# Packer template during image build.

EOL
$ echo -e '{"provider":"parallels"}\n' > ./metadata.json
$ tar cvzf ubuntu-(20|21).04.parallels.box ./ubuntu-(20|21).04-arm64.pvm  ./metadata.json ./Vagrantfile
```
