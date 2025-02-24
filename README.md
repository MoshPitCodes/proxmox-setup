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
- Basic understanding of IP networking

This list will likely grow over time and maybe some of the points will get a dedicated section in this repository.


# General
I will generally use the latest LTS or latest non LTS stable build. At the time of writing, these are the following:
- Ubuntu 24.04 LTS Desktop/Server
- Ubuntu 24.10 Stable Desktop/Server
- Ubuntu 24.04 Cloud Image (for use with `cloud-init`)
- Ubuntu 24.10 Cloud Image (for use with `cloud-init`)

For a list of available images, please see the following links:

| Version | Link to download |
| --- | --- |
| Ubuntu Desktop | https://ubuntu.com/download/desktop |
| Ubuntu Server | https://ubuntu.com/download/server |
| Ubuntu Cloud Images | List all new or modified files |

> Warning: Always verify downloaded images against an MD5/SHA256 checksum provided by the maintainer of the distribution.

# Use Case 1: Running LXC containers with Ubuntu
The first use case I came across then setting up my Proxmox host was to be able to run Ubuntu VMs and LXC containers with minimal effort. I knew that templating was a thing and in combination with `cloud-init`, I think I have found a solution that works for my purposes.

## Ubuntu LXC container: Download an Ubuntu image


## Ubuntu LXC container: Installation


## Ubuntu LXC container: Update


## Ubuntu LXC container: Removal of conflicting packages


## Ubuntu LXC container: Setup for `apt` repositories
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

## Ubuntu LXC container: Installion of the Docker Engine
To install the latest version of the Docker Engine on the system, run the following command:

```bash
# Install latest version of Docker Engine 
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
