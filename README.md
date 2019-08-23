# dcosup
This setup creates a nested VM using libvirt. It then installs Virtualbox and
Vagrant in the VM to use with minidcos](https://minidcos.readthedocs.io).

> NOTE: Currently libvirt only. Support for VirtualBox will be available soon

## Requirements

Install qemu-kvm, libvirt, vagrant-libvirt, and ansible

### Fedora

```
sudo dnf -y install qemu-kvm libvirt vagrant-libvirt ansible
```

You will also need to have kubectl on your system. You can install it by going
to https://kubernetes.io/docs/tasks/tools/install-kubectl/ .

### CentOS

* Run the following:

```
sudo yum install epel-release
sudo yum install qemu libvirt libvirt-devel ruby-devel gcc qemu-kvm ansible
```

* Install Vagrant: https://www.vagrantup.com/downloads.html
* Install the libvirt plugin for vagrant:

```
vagrant plugin install vagrant-libvirt
```

### Nested VM support

Modprobe options:

```
options kvm_intel nested=1 enable_apicv=n
options kvm ignore_msrs=1
```

Reboot the host, and then run the following commands.

```
# want Y to be returned
$ cat /sys/module/kvm/parameters/ignore_msrs

# want N to be returned
$ cat /sys/module/kvm_intel/parameters/enable_apicv

# want Y to be returned
$ cat /sys/module/kvm_intel/parameters/nested
```

[Source](https://fabianlee.org/2018/09/19/kvm-deploying-a-nested-version-of-vmware-esxi-6-7-inside-kvm)

## Usage
This setup sets up a nested VM with 32 G of RAM.

```
$ vagrant up
```
