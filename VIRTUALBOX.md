# Virtual Box for Ubuntu 20.104

## Install

```console
sudo apt update
sudo apt install -y virtualbox virtualbox-ext-pack
```

Unzip the .ova files.

## Convert .ova to Hyper-V

```console
VBoxManage clonehd --format vhd "Cargo-Cult-disk1.vmdk" "Cargo-Cult-disk1.vhd"
chmod +rwx Cargo-Cult-disk1.vhd
```