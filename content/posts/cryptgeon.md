---
title: "Cryptgeon"
date: 2022-06-02T15:48:41+02:00
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
If you are sharing passwords or other sensitive data over IM, email etc. you should take a look at this free web application. The application is called cryptgeon and is developed by a guy called [Nicco](https://github.com/cupcakearmy). The application will only keep the shared secrets/files in memory and not write the data to disk. You can have a look at his GitHub repo [here](https://github.com/cupcakearmy/cryptgeon) or see the screenshot below for the UI.

[![cryptgeon](/img/posts/cryptgeon.png)](/img/posts/cryptgeon.png)

## Docker Compose
If you are using docker engine and docker-compose here's the compose file I'm using to run the application.
```yaml
version: '3.7'

services:
  memcached:
    image: memcached:1-alpine
    entrypoint: memcached -m 128M -I 4M # Limit to 128 MB Ram, 4M per entry, customize at free will.

  app:
    image: cupcakearmy/cryptgeon:latest
    depends_on:
      - memcached
    environment:
      SIZE_LIMIT: 4M
    ports:
      - 82:5000
    restart: unless-stopped
```