---
title: "Docker Hosting"
date: 2022-05-25T09:07:02+02:00
draft: false
toc: true
images:
tags:
  - docker
  - linux
  - portainer
  - proxmox
  - nginx
  - opensource
  - selfhosted
---
## Introduction
All of the my lab & hosting needs are done thru various open source products. I like using docker engine & docker-compose for quickly getting products spun up. I've had a look at using [k8s](https://kubernetes.io) instead, but for home usage and my needs I think it is to much. In the setup I also have a external vps which is hosting this website as one of the products. Below I'll run thu all the products I'm using.
## Architecture Overview
Below is an overview of how I have done my setup. Basicly all vm/lxc's are deployed with Ubuntu 22.04, then docker-engine and docker-compose, portainer ce for controling the environments from one central location and nginx proxy manager to control url's, certificates (let's encrypt) and routing to hosts.
```
proxmox-ha-cluster  
│
└───proxmox-host1
│   │
│   └───proxmox-vm
│       │   docker-engine
│       │   docker-compose
│       │   portainer-main
│       │   nginx-proxymanager
│       │   app-a
│       │   app-b
│       │   app-c
│
└───proxmox-host2
│   │
│   └───proxmox-lxc
│       │   docker-engine
│       │   docker-compose
│       │   portainer-agent
│       │   nginx-proxymanager
│       │   app-a
│       │   app-b
│       │   app-c
│
external-kvm-host
│
└───external-vps
    │
    └───external-vm
        │   docker-engine
        │   docker-compose
        │   portainer-agent
        │   nginx-proxymanager
        │   app-a
        │   app-b
        │   app-c
```
## Proxmox
I use [Proxmox](https://www.proxmox.com/en/) as the hypervisor at home. I switches from VMware ~2 years ago and have not looked back since. One of the benefits I like with Proxmox is the ability to deploy LXC containers out of the box. I have 2 hosts at home, setup in a HA Cluster for failover.
## Docker & docker-compose
I think [docker](https://www.docker.com/) is known to most people working with container environments. Together with docker compose, it is perfect for quickly deploying new apps in your infrastructure.  
## Portainer CE
[Portainer](https://www.portainer.io/) is a container management platform. It comes in 2 flavours, a paid (business) edition and then the free one called portainer ce. In my own setup I have 1 portainer ce app running, and then the 2 other hosts are linked up thru the portainer agent.
## Nginx Proxy Manager
[Nginx Proxy Manager](https://nginxproxymanager.com/) is (as the name states) a proxy manager similar to [Traefik](https://traefik.io). I use it on all the docker engine hosts to control certificates, routing & all the url's.
## Links & Resources
Below you can find some usefull links and doc's to get started on a setup similar to the above.
### Proxmox
[Install Proxmox VE](https://pve.proxmox.com/wiki/Installation)  
[Dark theme for Proxmox VE](https://github.com/Weilbyte/PVEDiscordDark)  
[Remove Proxmox subscription warning](https://johnscs.com/remove-proxmox51-subscription-notice/)
### Docker & docker-compose
[Install docker engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)  
[Install docker compose on Ubuntu](https://docs.docker.com/compose/install/compose-plugin/)
### Nginx Proxy Manager
[Install Nginx Proxy Manager](https://nginxproxymanager.com/setup/)
## Screenshots
Portainer CE UI.
[![Portainer](/img/posts/portainer.png)](/img/posts/portainer.png)