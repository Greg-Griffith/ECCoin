Gitian build
============

This is guide take for granted that you are using Ubuntu bionic 18.04 as host OS. the aim of the document is to be able to produce deterministic binaries using gitian-tools and docker containers.


Prerequisite
-------------

These are steps that as to be executed once and that don't need to be repeated for every new gitian build process.

```bash
sudo apt install git apt-cacher-ng ruby docker.io
sudo usermod -a -G docker $USER
exec su -l $USER  #make effective the usermod command
cd ~/src
git clone https://github.com/project-ecc/eccoin.git
git clone https://github.com/devrandom/gitian-builder.git
cd gitian-builder
bin/make-base-vm --suite bionic --arch amd64 --docker
```

Build the binaries
------------------

These are the commands to actually roduce the executable:

```bash
cd ~/src/gitian-builder
export USE_DOCKER=1
bin/gbuild -j 4 -m 10000 --url bitcoin=https://github.com/rpoject-ecc/eccoin.git --commit bitcoin=dev ../eccoin/contrib/gitian-descriptors/gitian-linux.yml
```

Your binaries will be ready to be used in `build/out/` folder.
