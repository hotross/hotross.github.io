---
layout: post
title: "Local Git and Runners"
date: 2025-01-26 07:00:00 +1000
tags: [automation, linux, docker]
categories: [work]
author: Ross
image: 
  path: /assets/img/posts/gitea.png
---
# Self-Hosted CI/CD with Gitea Actions: A Docker Compose Guide

This guide walks you through setting up a complete, self-hosted CI/CD environment using Gitea, Gitea Actions Runner, and PostgreSQL, all managed with Docker Compose.  The actual documentation for Gitea is very comprehensive but doing so a lot gets lost in the weeds. thisis the config i have used to make stuff ACTUALLY work.

## Prerequisites

Before you begin, make sure you have the following installed on your system:

*   **Docker:**  Follow the official Docker installation guide for your operating system ([https://docs.docker.com/engine/install/ubuntu/](https://docs.docker.com/engine/install/ubuntu/) - you provided the Ubuntu link, so I'm assuming that's your OS.  Adapt if necessary).
*    **Basic Command-Line Familiarity**

Make sure the docker daemon is running and you have done the post install steps listed on the docker website to change folder and group owners. It makes things alot easier

## Step 1: Project Setup

1.  **Create a Project Directory:**
    ```bash
    mkdir gitea-actions-setup
    cd gitea-actions-setup
    ```

2.  **Create Directories for Data Persistence:**
    ```bash
    mkdir -p ./gitea ./postgres ./runners
    ```
    These directories will store Gitea's data, the PostgreSQL database, and runner configurations, respectively.  This ensures your data survives container restarts and upgrades.

## Step 2: Create the `docker-compose.yml` File

Create a file named `docker-compose.yml` in your `gitea-actions-setup` directory and paste the following configuration:

```yaml

networks:
  gitea_net:  # Define a custom network for our services

services:
  server:
    image: docker.io/gitea/gitea:nightly  # Use the nightly build (consider 'latest' for production)
    container_name: gitea
    environment:
      - USER_UID=1000  # Important for file permissions
      - USER_GID=1000
      - GITEA__database__DB_TYPE=postgres
      - GITEA__database__HOST=db:5432  # Connect to the 'db' service
      - GITEA__database__NAME=gitea
      - GITEA__database__USER=gitea
      - GITEA__database__PASSWD=gitea
    restart: always
    networks:
      - gitea_net
    volumes:
      - ./gitea:/data  # Persist Gitea data
      - /etc/timezone:/etc/timezone:ro  # Set timezone (important for logs)
      - /etc/localtime:/etc/localtime:ro
    ports:
      - "3000:3000"  # Expose Gitea's web interface
      - "222:22"    # Expose SSH port (optional, but useful)
    depends_on:
      - db

  db:
    image: docker.io/library/postgres:14  # Use PostgreSQL 14
    restart: always
    environment:
      - POSTGRES_USER=gitea
      - POSTGRES_PASSWORD=gitea
      - POSTGRES_DB=gitea
    networks:
      - gitea_net
    volumes:
      - ./postgres:/var/lib/postgresql/data  # Persist PostgreSQL data

  runner:
    image: docker.io/gitea/act_runner:nightly
    environment:
      CONFIG_FILE: /config.yaml
      GITEA_INSTANCE_URL: "http://gitea:3000"  # Use the 'gitea' service name
      GITEA_RUNNER_REGISTRATION_TOKEN: "registration token" # REPLACE THIS!
      GITEA_RUNNER_NAME: "runner"
    networks:
      - gitea_net
    depends_on:
      - db
      - server
    volumes:
      - ./config.yaml:/config.yaml  # Mount the runner config
      - ./runners:/data #persist runner file
      - /var/run/docker.sock:/var/run/docker.sock  # Allow Docker-in-Docker

```
## gitea-actions-setup directory:

here is the config.yaml 

YOU NEED THE CONFIG FILE. every thing on the internet says you dont but if you dont specify the network you wont be able to pull repos from gitea. USE THE CONFIG FILE.

```YAML


log:
  level: info  # You can change this to 'debug' for more verbose logs

runner:
  file: .runner
  capacity: 1  # Number of concurrent jobs
  envs: {} # Add any global environment variables here
  env_file: ""  # Or specify a .env file
  timeout: 3h
  shutdown_timeout: 0s
  insecure: false
  fetch_timeout: 5s
  fetch_interval: 2s
  labels:
    - "ubuntu-latest:docker://gitea/runner-images:ubuntu-latest"  # Keep at least one label
    - "ubuntu-22.04:docker://gitea/runner-images:ubuntu-22.04"
    - "ubuntu-20.04:docker://gitea/runner-images:ubuntu-20.04"

cache:
  enabled: true
  dir: ""
  host: ""
  port: 0
  external_server: ""

container:
  network: "gitea_gitea_net"  # VERY IMPORTANT: Use the network name from docker-compose.yml
  privileged: false # Set to 'true' if you need Docker-in-Docker and privileged mode.
  options: {}
  workdir_parent: ""
  valid_volumes:
    - '**'  # Allow mounting any volume (for simplicity, but be cautious in production)
  docker_host: "" # Leave empty to automatically detect the Docker host
  force_pull: true
  force_rebuild: false

host:
  workdir_parent: "" # use default

```

### Important Changes:
container.network: Ensure this matches the networks key in your docker-compose.yml file (e.g., gitea_gitea_net). This is critical for the runner to communicate with Gitea.
you might look at that and think "oh thats wrong" it is not this is how docker defaults names networks.


```Bash

docker compose up -d
```


## Test Workflow
in your repo make a directory called.gitea/workflows
in there make a file called demo.yaml

```YAML
name: Test Workflow

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest  # Use a label matching your runner's configuration
    steps:
      - uses: actions/checkout@v3
      - run: echo "Hello from Gitea Actions!"
      - run: uname -a
```

when you push the file to gitea it should now run the actions. From here on documentation is your friend have a look at some examples of what you can do with this

## Notes
- Dont use the SSH stuff if your using docker it is a pain in the butt to get the keys configured and you would only be locally hosting this so using http isnt a big deal


