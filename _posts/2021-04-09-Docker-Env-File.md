---
layout: post
title:  "Securing Docker Environment Variables"
excerpt: >- 
    Quick tutorial on how to secure your sensitive environment variables for your Docker containers.
tag: 
- docker
- tutorial
toc: False
updated: 2021-04-10
---

## Securing Environment Variables

It is generally bad practice to define sensitive information such as passwords (i.e. `JUPYTER_TOKEN`) directly within your `docker-compose.yml`. Anyone who can see your file, then has access to your sensitive information. Instead, it is suggested you store this data in a `.env` file. For example, if you make a file called `.env` in your project directory with the following line:

```shell
JUPYTER_TOKEN=jupyter
```

Here we specify a variable called `JUPYTER_TOKEN` and assign it the value `jupyter`. Next, make the following change to your `docker-compose.yml` file:

```yaml
services:
    service-a:
        ...
        environment:
            - JUPYTER_TOKEN=$(JUPYTER_TOKEN)
        ...
```

When you `docker-compose` `build` or `up`, the service will reference your `.env` file and look for the variable within the `${...}`. Therefore, you can store your sensitive data in a `.env` file and keep that protected.

## Specifying More Environment Files

If you would like to store your information in other files&mdash;besides `.env` files&mdash;you have a few options.

One option is to specify the alternative file in the `docker-compose` CLI.

```shell
docker-compose --env-file /path/to/file
```

Another option is to specify within the `docker-compose.yml` service,

```yaml
services:
    service-a:
        ...
        env_file:
            - /path/to/file
        ...
```