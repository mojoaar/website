---
title: "Code Server"
date: 2022-05-13T18:44:42+02:00
draft: false
toc: true
images:
tags:
  - docker
  - application
  - compose
  - security
  - opensource
  - selfhosted
---
## Introduction
I've been using VS Code as my primary editor for years and love using it. Emagine taking that experience to the browser and running VS Code with a consistent development environment?...you can - with the docker engine and [code-server](https://github.com/coder/code-server)! Actually this how I manage and maintain my site here at [technet.cc](https://technet.cc). Thanks to the good folks at [linuxserver.io](https://www.linuxserver.io/) who have made a ready to run [container](https://fleet.linuxserver.io/image?name=linuxserver/code-server) it is super easy getting it setup and running with the docker engine & docker-compose. In the compose file below I make sure to map in my homedir, so I can access the files located in the development folder. The site is running on [Hugo](https://gohugo.io/) and I have it setup against GitHub for source control. The VS Code terminal is connected to the actual VPS thru ssh, so I have access to all the Hugo command for publishing.
## Docker Compose
If you are using docker engine and docker-compose here's the compose file I'm using to run the application.
```yaml
version: "2.1"
services:
  code-server:
    image: lscr.io/linuxserver/code-server:latest
    container_name: code-server
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Copenhagen
      - PASSWORD=SuperSecretPassword #optional
      - HASHED_PASSWORD= #optional
      - SUDO_PASSWORD=SuperSecretPassword #optional
      - SUDO_PASSWORD_HASH= #optional
      - PROXY_DOMAIN=code.domain.com #optional
      - DEFAULT_WORKSPACE=/config/workspace #optional
    volumes:
      - /home/<username>/code-server/config:/config
      - /home/<username>/development:/development
    ports:
      - 8443:8443
    restart: unless-stopped
```
## Screenshots
Working on this actual blog post in the browser with code server.
[![Code Server](/img/posts/code-server.png)](/img/posts/code-server.png)