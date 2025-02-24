# Proxmox Setup
Collection of my experiences, CLI commands and configurations for running a homelab server on Proxmox VE.


# Motivation
I have recently started to get interested more in setting up a homelab for learning a couple of things from hands-on experience. Running Docker in a Ubuntu LXC container on a Proxmox host was the first use case I had. After some research, I want to summarize my findings and add some context to what I was doing for the setup.


# Pre-requisites
Throughout this repository, I will assume things:
- Bare-metal installation of Proxmox VE on a host is done
- Basic configuration of Proxmox VE is done
- Basic understanding on setting up and configuring LXC containers on a Proxmox VE host
- Basic understanding of Container Templates (CT Templates) on a Proxmox VE host


# Setup
## Installing Ubuntu in LXC container


## Updating the Ubuntu LXC container



## Uninstalling conflicting packages



## Setting up apt repositories
First, we need to add the official GPG keys from Docker to our keyrings:
```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

Now we need to add the official repositories to the `apt` sources:111111111111111
```bash
# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

Run the following command to update the `apt` repositories:
```bash
# Update
sudo apt-get update
```

## Installing the Docker Engine
To install the latest version of the Docker Engine on the system, run the following command:

```bash
# Install latest version of Docker Engine 
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
