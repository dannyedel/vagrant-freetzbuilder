# Freetzbuilder Vagrant VM

The purpose of this VM is to have a well-defined and
reproducible environment to build the freetz image
for my Fritzbox with.

## Preparation

In this folder, call `vagrant up` for the first-time
setup.

To update system packages and svn repo, call
`vagrant provision`.

## Building

Call `vagrant ssh` to enter an interactive shell inside
the VM.

* `cd freetz`
* if you want to make sure its clean: `make distclean`
* `make menuconfig`
* `make`
* Get coffee

## Give me back my hard drive space

Don't forget to save `~/freetz/.config` and any built
images to your host before you do this.

To delete the VM and restore the HDD space, call

* `vagrant destroy`
