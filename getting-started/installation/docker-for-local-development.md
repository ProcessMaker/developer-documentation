---
description: >-
  Install open-source ProcessMaker Platform using Docker Desktop and Docker
  Compose.
---

# Docker for Local Development

verview

Install the open-source ProcessMaker Platform using [Docker Desktop](https://www.docker.com/products/docker-desktop/) and [Docker Compose](https://docs.docker.com/compose/). Before proceeding with the installation process, it is essential to have a basic understanding of Linux commands. Familiarity with common command-line operations such as navigating directories, executing commands, and editing files will greatly facilitate the installation process and troubleshooting.

## Requirements

Before proceeding with the installation, ensure that you have met the following prerequisites.

<table data-full-width="false"><thead><tr><th>Requirement</th><th width="234">Function</th><th width="94">Version</th><th>Installation Guide</th></tr></thead><tbody><tr><td><a href="https://learn.microsoft.com/en-us/windows/wsl/install">WSL2</a> or Unix based OS</td><td>WSL2 enables access to the command line for installing and accessing containers.</td><td>Latest</td><td><a href="https://learn.microsoft.com/en-us/windows/wsl/install">Setting up WSL2</a></td></tr><tr><td><a href="https://www.docker.com/products/docker-desktop/">Docker</a></td><td>Docker provides the underlying technology to deploy containerized applications.</td><td>Latest</td><td><a href="https://docs.docker.com/get-docker/">Setting up Docker</a></td></tr></tbody></table>

### WSL2 (Windows Subsystem for Linux)

If you are using Microsoft Windows, then you can install ProcessMaker within WSL2.

Go to [Microsoft's site](https://learn.microsoft.com/en-us/windows/wsl/install) and follow their instructions. It's very easy and quick.

### Docker

Download and install [Docker for Desktop](https://www.docker.com/products/docker-desktop/).

{% hint style="success" %}
If you are on Microsoft Windows, ensure to go into settings and enable the WSL2 integration.
{% endhint %}

## Docker Compose

This installation procedure uses Docker Compose. The Docker Compose file is located in this [GitHub repository](https://github.com/ProcessMaker/pmcore-docker). Issues, PRs and contribution are most welcome!

### The Docker Compose File

{% hint style="danger" %}
Ensure you specify which branch or release of the ProcessMaker repository you wish to install and replace `${PROCESSMAKER_CORE_VERSION_INSTALL}` with the desired version.
{% endhint %}

Open up your terminal for your platform:

* **Windows:** Windows Terminal is a good option. Just make sure you don't go into CMD or PowerShell.
* **Macs:** iTerm is a good option.
* **Other Unix-based operating systems:** The native terminal should be more than adequate.

{% hint style="success" %}
Oh My Zsh is a wonderful CLI tool that can help you with auto-completion within the terminal and syntax highlighting, convenience methods and much more.

You can find information about [installing it here.](https://ohmyz.sh/)
{% endhint %}

The yaml file below is the `docker-compose.yaml` file that we are going to use.

{% code overflow="wrap" fullWidth="false" %}
```yaml
version: '3.3'
networks:
    processmaker:
volumes:
    docker-data:
    redis-data:
services:
    mysql:
        image: mysql:8
        platform: linux/amd64
        ports:
            - '3306:3306'
        security_opt:
            - seccomp:unconfined
        environment:
            MYSQL_ROOT_PASSWORD: C0mpliCat3dPassW0rd
            MYSQL_DATABASE: pm4
            MYSQL_USER: pm4_user
            MYSQL_PASSWORD: pm4_password
        networks:
            - processmaker
        volumes:
            - ./mysql-data:/var/lib/mysql
        restart: always
        healthcheck:
            test: [ 'CMD', 'mysqladmin', 'ping', '-u', 'root', '-p${MYSQL_ROOT_PASSWORD}' ]
            interval: 30s
            timeout: 10s
            retries: 5
    phpmyadmin:
        depends_on:
            - mysql
        image: phpmyadmin/phpmyadmin
        environment:
            PMA_HOST: "mysql"
            PMA_ARBITRARY: 1
        ports:
            - '8080:80'
        networks:
            - processmaker
    redis:
        image: redis:6
        command: redis-server --save 60 1 --loglevel warning
        ports:
            - '6379:6379'
        networks:
            - processmaker
        volumes:
            - redis-data:/data
        restart: always
        healthcheck:
            test: [ 'CMD', 'redis-cli', 'ping' ]
            interval: 30s
            timeout: 10s
            retries: 5
    docker:
        image: docker:20-dind
        privileged: true
        ports:
            - '2375:2375'
        networks:
            - processmaker
        volumes:
            - docker-data:/var/lib/docker
            - ./scripts:/opt/scripts
        environment:
            DOCKER_DRIVER: "overlay2"
            DOCKER_TLS_CERTDIR: ""
        restart: always
        healthcheck:
            test: [ 'CMD', 'docker', 'info' ]
            interval: 30s
            timeout: 10s
            retries: 5
    processmaker:
        image: processmaker/pm4-dev:4.3v1
        ports:
            - '80:80'
            - '6001:6001'
        depends_on:
            mysql:
                condition: service_healthy
            redis:
                condition: service_healthy
            docker:
                condition: service_healthy
        networks:
            - processmaker
        volumes:
            - ./processmaker:/opt/processmaker
            - ./env:/opt/.env
            - ./scripts:/opt/scripts
        environment:
            PM_branch: ${PROCESSMAKER_CORE_VERSION_INSTAll}
            WAIT_FOR_DEPENDENTS: 1
            DOCKER_HOST: 'tcp://docker:2375'
            NO_PROXY: "127.0.0.1,localhost,docker:2375"

```
{% endcode %}

### The Laravel ENV File

Below is the default configuration parameters for the `.env` file (which will be `env` if cloning from the repo). You can copy-and-paste the snippet below into a new file. If you are using the repository, it should already be set there.

{% code overflow="wrap" fullWidth="false" %}
```
APP_URL=http://localhost
DOCKER_HOST_URL=https://localhost
BROADCASTER_HOST=http://localhost:6001
LARAVEL_ECHO_SERVER_AUTH_HOST=http://localhost
APP_KEY=base64:bCBJXXFbO/dgnlaJvQPLKWWE/dzhsn1+ylOS5vm9zxc=
APP_DEBUG=TRUE
DEBUGBAR_ENABLED=FALSE
APP_NAME=ProcessMaker
APP_ENV=local
DB_HOSTNAME=mysql
DB_DATABASE=pm4
DB_USERNAME=pm4_user
DB_PASSWORD=pm4_password
DB_PORT=3306
DATA_DB_DRIVER=mysql
DATA_DB_HOST=mysql
DATA_DB_DATABASE=pm4
DATA_DB_PORT=3306
DATA_DB_USERNAME=pm4_user
DATA_DB_PASSWORD=pm4_password
APP_TIMEZONE=UTC
DATE_FORMAT="m/d/Y H:i"
MAIN_LOGO_PATH="/img/processmaker_logo.png"
ICON_PATH_PATH="/img/processmaker_icon.png"
LOGIN_LOGO_PATH="img/processmaker_login.png"
CACHE_DRIVER=redis
BROADCAST_DRIVER=redis
REDIS_PORT=6379
REDIS_HOST=redis
HOME=/opt/processmaker
HORIZON_PREFIX=pm4:
BROADCASTER_KEY=21a795019957dde6bcd96142e05d4b10
LARAVEL_ECHO_SERVER_PORT=6001
LARAVEL_ECHO_SERVER_DEBUG=TRUE
LARAVEL_ECHO_SERVER_PROTO=http
LARAVEL_ECHO_SERVER_REDIS_HOST=redis
LARAVEL_ECHO_SERVER_REDIS_PORT=6379
DOCKER_HOST=tcp://docker:2375
PROCESSMAKER_SCRIPTS_DOCKER_HOST=tcp://docker:2375
PROCESSMAKER_SCRIPTS_HOME=/opt/scripts
API_SSL_VERIFY=0
PROXIES=*
LOGOUT_OTHER_DEVICES=false
BROWSER_CACHE=true
API_TIMEOUT=5000
SESSION_DRIVER=redis
SESSION_SECURE_COOKIE=false
```
{% endcode %}

You may change any settings that you wish. Just make sure that the settings are valid and do not cause errors or issues.

In your terminal, run the following Docker command inside the folder where your Docker Compose file is:

```
docker-compose up
```

To spin down the environment, run the following Docker command:

```
docker-compose down
```

{% hint style="warning" %}
If this is your first time installing, it will take time for all the Docker images to download. At the end, you should see a message in your terminal that shows the Laravel Echo server is running and initial jobs should start running.
{% endhint %}

## Did You Know?

The script adds a mounted folder for the ProcessMaker Platform installation and for Scripts, which is basically a good place to stick anything that is not purely ProcessMaker that you need as part of your application. For example, if you are developing a custom package or using Script Executors.

You may access the filesystem from outside the container. Just make sure to run any commands like `composer update` within the container (or send the command to it).

## Troubleshooting

{% hint style="info" %}
This section will be updated regularly as new issues and troubleshooting steps become known.
{% endhint %}

## Feedback



If you got all the way down here, congratulations on being thorough! If you could kindly rate this page as helpful or unhelpful, that goes a long way towards improving our content.

## Quick Start with Process Templates

Explore our ready-to-go Process Templates to kick-start your automation across several use cases and industries. Deploy into your Platform instance to spin up new processes and use as-is with all necessary assets included.

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-cover data-type="files"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><mark style="color:blue;">How to import Process Templates</mark></td><td></td><td></td><td><a href="../../.gitbook/assets/Untitled.png">Untitled.png</a></td><td><a href="https://processmaker.gitbook.io/processmaker/designing-processes/viewing-processes/manage-process-templates/import-and-configure-a-process-template">https://processmaker.gitbook.io/processmaker/designing-processes/viewing-processes/manage-process-templates/import-and-configure-a-process-template</a></td></tr><tr><td><mark style="color:blue;">Download Process Templates</mark></td><td></td><td></td><td><a href="../../.gitbook/assets/all processes.png">all processes.png</a></td><td><a href="https://www.processmaker.com/resources/customer-success/templates/">https://www.processmaker.com/resources/customer-success/templates/</a></td></tr></tbody></table>
