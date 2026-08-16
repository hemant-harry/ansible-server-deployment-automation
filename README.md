# Ansible Server Deployment Automation

Ansible-based automation project for configuring and deploying a PHP web application on multiple web servers using a reusable Ansible role.

## Architecture

```text
                    GitHub Repository
                           |
                           | Git
                           ↓
                  Ansible Control Node
                           |
                    SSH Key Authentication
                    ┌──────┴──────┐
                    ↓             ↓
              Web Server 1   Web Server 2
              Apache + PHP    Apache + PHP
                    |             |
                    └──────┬──────┘
                           ↓
                        Browser
```

## Features

* Ansible role-based project structure
* One control node and two target web servers
* SSH key-based communication
* Project-level `ansible.cfg`
* Custom inventory
* Package installation using variables and loops
* Apache and PHP installation
* Git-based application deployment
* Repository URL managed through Ansible variables
* Jinja2 templates for dynamic server information
* Handlers with `notify` for Apache restart
* Automatic application update when the Git repository changes

## Project Structure

```text
project/
├── ansible.cfg
├── inventory
├── deploy.yml
├── README.md
│
└── website/
    ├── defaults/
    │   └── main.yml
    ├── files/
    ├── handlers/
    │   └── main.yml
    ├── meta/
    ├── tasks/
    │   └── main.yml
    ├── templates/
    ├── tests/
    └── vars/
```

## How It Works

The `deploy.yml` playbook calls the `website` role.

The role:

1. Installs required packages.
2. Deploys the application from GitHub.
3. Configures the web server.
4. Deploys dynamic content using Jinja2 templates.
5. Notifies the Apache handler when required.
6. Restarts Apache when a relevant configuration or deployment change occurs.

## Run the Project

From the project directory:

```bash
ansible-playbook deploy.yml
```

Run only installation tasks:

```bash
ansible-playbook deploy.yml --tags install
```

Run only deployment tasks:

```bash
ansible-playbook deploy.yml --tags deploy
```

Run configuration tasks:

```bash
ansible-playbook deploy.yml --tags config
```

List available tasks:

```bash
ansible-playbook deploy.yml --list-tasks
```

List available tags:

```bash
ansible-playbook deploy.yml --list-tags
```

## Technologies

* Ansible
* Linux
* Apache HTTPD
* PHP
* Git / GitHub
* Jinja2
* SSH

## Project Goal

The goal of this project is to practice real-world Ansible automation concepts such as reusable roles, variables, loops, templates, handlers, notifications, tags, SSH-based communication, and Git-based application deployment.
