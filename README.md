# QEMU
QEMU is an open source machine emulator and virtualizer. 

See [QEMU](https://www.qemu.org/)

See [Install](INSTALL.md) for configuration of a Ubuntu VM.

Before setting up the emulation when trying to execute a program compiled for a different architecture:

```console
$ uname -m                                   # Display the host architecture
x86_64

$ docker run --rm -t arm64v8/ubuntu uname -m # Run an executable made for aarch64 on x86_64

WARNING: The requested image's platform (linux/arm64) does not match the detected host platform (linux/amd64) and no specific platform was requested
standard_init_linux.go:219: exec user process caused: exec format error
```

As expected the instructions are not recognized since the packages are not installed yet. Installing the following packages should allow you to enable support for `aarch64` containers on your `x86` workstation:

```console
$ sudo apt-get install qemu binfmt-support qemu-user-static              # Install the qemu packages
$ docker run --rm --privileged multiarch/qemu-user-static --reset -p yes # This step will execute the registering scripts
$ docker run --rm -t arm64v8/ubuntu uname -m                             # Testing the emulation environment aarch64

WARNING: The requested image's platform (linux/arm64) does not match the detected host platform (linux/amd64) and no specific platform was requested
aarch64 # -> No exec format error
```

The installation was successful, the emulation is working. At this point, we can now run aarch64 programs on the host x86_64 workstation.

Pull Docker images for the jetson onto the `x86` platform

```console
docker pull nvcr.io/nvidia/l4t-base:r32.2.1
docker pull stereolabs/zed:3.0-devel-jetson-jp4.2
```

https://www.stereolabs.com/docs/docker/building-arm-container-on-x86/

https://www.stereolabs.com/docs/docker/install-guide-jetson/

https://hub.docker.com/r/balenalib/jetson-nano-node

node with jetson nano containers