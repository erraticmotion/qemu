# Install

## Docker

```console

sudo apt-get update
sudo apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io
sudo usermod -aG docker $USER
su -l $USER
```

## Configure the Docker daemon in the VM to allow remote connections

```console
# These commands get run inside of your VM.

# Create the directory to store the configuration file.
sudo mkdir -p /etc/systemd/system/docker.service.d

# Create a new file to store the daemon options.
sudo nano /etc/systemd/system/docker.service.d/options.conf

# Now make it look like this and save the file when you're done:
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd -H unix:// -H tcp://0.0.0.0:2375

# Reload the systemd daemon.
sudo systemctl daemon-reload

# Restart Docker.
sudo systemctl restart docker
```

## Docker Compose

```console
sudo curl -L "https://github.com/docker/compose/releases/download/1.25.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

## Support KVM
```console
sudo apt install -y qemu-kvm
sudo apt install -y cpu-checker
kvm-ok
sudo apt install -y acl
sudo setfacl -m u:${USER}:rw /dev/kvm
```

## Install QEMU
```console
sudo apt-get install -y qemu
```

## Upgrade
```console
sudo apt-get upgrade -y
```