Dockerized GITLAB & CI/CD

![Alt Text](https://media.giphy.com/media/hQWYZpZCHKWIM/giphy.gif)

Usage
=====

Set values for env variables in the .env file, like as follow
    
    PUBLISH_PORT_HTTP=80
    PUBLISH_PORT_HTTPS=443

    SSL=ssl
    
    GITLAB_EXTERNAL_SCHEMA=http or https
    GITLAB_EXTERNAL_HOST=git.example.com
    GITLAB_EXTERNAL_PORT=80
    
    GITLAB_PUBLISH_PORT_SSH=22
    
    GITLAB_CONF=/example/git/config
    GITLAB_LOGS=/example/git/logs
    GITLAB_RUNNER=/example/git/data
    
    REGISTRY_EXTERNAL_HOST=registry.example.com
    REGISTRY_DATA=/example/registry/data

    REGISTRY_LOGIN=
    REGISTRY_PASSWD=
    
    GITLAB_RUNNER=/example/git/runner
    
    PROXY_LOGS=/exaple/proxy/logs

Read .env:

    $ source .env 

Build images:


    $ docker-compose build

Start services:


    $ docker-compose up -d

Down services:


    $ docker-compose down

FYI
===
>>>
Before using this, be sure to ask for the blessing from Ali. :tada:

Gitlab runner config: ci/config.toml

Also If you want to use ssl certificate, add environment variable `SSL=ssl` (or `non-ssl` for non-secure connection) please generate that under the `cert` directory.
>>>


