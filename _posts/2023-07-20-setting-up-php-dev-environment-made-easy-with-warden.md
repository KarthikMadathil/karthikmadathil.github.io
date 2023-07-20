---
layout: post
title:  "Setting up PHP dev environment made easy with Warden & Docker"
author: karthik
featured: true
date:   2023-07-20 11:53:52 +0530
categories: [ PHP, Debug ,Docker ,Dev , DevEnvironment, Tools,Mysql,Nginix, Tutorial , Debugging , Coding]
image: assets/images/warden-php-dev.png
comments: false
---  

Setting up a development environment can be a tedious and time-consuming task. It requires installing and configuring various tools and dependencies. However, with **Warden**, you can set up your development environment in seconds


# What is warden ?

Warden is a CLI utility for orchestrating Docker-based developer environments. It enables multiple local environments to run simultaneously without port conflicts via the use of a few centrally run services for proxying requests into the correct environment’s containers. Warden has features like Traefik for SSL termination and routing/proxying requests into the correct containers, Portainer for quick visibility into what’s running inside the local Docker host, Dnsmasq to serve DNS responses for .test domains eliminating manual editing of /etc/hosts, and an SSH tunnel for connecting from Sequel Pro or TablePlus into any one of multiple running database containers.

Warden is easy to install and use. You can install it using Homebrew on macOS or Linux. Once installed, you can create a new environment by running the  `warden env-init <project_name> <environment_type>`  command. You can specify the environment type, Docker image, and other options using flags.

## Prerequisites

 Simply  a Docker Desktop for Mac 2.2.0.0 or later or Docker for Linux  or Docker for Windows
To install Docker  you can refer [Official Docker Docs](https://docs.docker.com/engine/install/) or refer some order sites

## Installation

Here i'll be discussing about installtion in Ubuntu ,For any other  Os  you can refer [here](https://docs.warden.dev/installing.html)  .

Warden may be installed by cloning the repository to the directory of your choice and adding it to your `$PATH`. This method of installation may be when Homebrew does not already exist on your system or when preparing contributions to the Warden project.
  

    sudo  mkdir  /opt/warden
    sudo  chown  $(whoami)  /opt/warden
    git  clone  -b  main  https://github.com/wardenenv/warden.git  /opt/warden
    echo  'export  PATH="/opt/warden/bin:$PATH"'  >>  ~/.bashrc
    PATH="/opt/warden/bin:$PATH"
    warden  svc  up

 ####  Setting DNS
Now configure your DNS to resolve *.test to 127.0.0.1 or use /etc/hosts 

For that,  
Edit Hosts by

> sudo nano /etc/hosts

Then  Add

> 127.0.0.1                 *test

![](https://lh6.googleusercontent.com/XhB8SO-RBSzFgXmGMtp95UBLO64xVnncyA4blkWotAEvttO21t1RaC_skCWKMgvNESP046DYMOeAgbw4hMWiD4vrGswr4qHg9tuE_cVJ7vc44aQ4fTHevh6MZpJMLGN1kP5I64L-Deby3fA96kW1OVY)

  

**Note** : By default while initialising a project warden make a host like <project_name>.test
 
  #### Install SSL Certificate 

Download Certificate from   
> ~/.warden/ssl/rootca/certs/ca.cert.pem

Copy to 

> /usr/local/share/ca-certificates

 
Import Certifiacate to browser (Chrome) 

go to Chrome Settings -> Privacy And Security -> Manage Certificates (see more) -> Authorities -> Import and select ~/.warden/ssl/rootca/certs/ca.cert.pem for import, then reload the page.

![](https://lh6.googleusercontent.com/t0q5IRItC9aZz4kYH-UX87Pn9iHWaKZCpyKPN3DLR0rDxqTe5J476vmZ23w19sGbGdQ-gwE2B3otN8TjVdMyKf32j9p_5pv0-NCRObbQxyZOiQtUWaLwPn0eJjoH_6xFCx0PNQCSE8_lfdZIdrk0kLc)
 

## Start Project 

#### Initialise The environment 

Goto any folder where you want to initialise the project 

    warden env-init <project_name> <environment_type>

Let check by installing wordpress. 

    warden env-init wptestwar wordpress

  

Now .env file will be created at the project root. This env file contains the configuration information of whole enviornment 

On that you can change the environment configuration as your wish.
Like your desired version **PHP** ,**MYSQL** etc.

#### Buid Project environment.

Use below command from the root directory to start the container.

      warden svc up

#### Initialise Project

Now download the wordpress files and extract to the project root directory 
Change wp-config.php configuration based on the auto generated .env file  

Now visit **wptestwar.test**
 
For more installation instructions goto [Docs](https://docs.warden.dev/environments.html) 

# Conclusion 

Warden is an excellent tool for developers who want to set up their development environment quickly and easily. With its features like Traefik, Portainer, Dnsmasq, and SSH tunnel, you can create multiple local environments without port conflicts and connect to them easily. and also provides Xdebug functionality & almost all variety of PHP environments such as -
-   [Drupal](https://docs.warden.dev/environments/types.html#drupal)
-   [Laravel](https://docs.warden.dev/environments/types.html#laravel)
-   [Magento 2](https://docs.warden.dev/environments/types.html#magento-2)
-   [Magento 1](https://docs.warden.dev/environments/types.html#magento-1)
-   [Shopware](https://docs.warden.dev/environments/types.html#shopware)
-   [Symfony](https://docs.warden.dev/environments/types.html#symfony)
-   [WordPress](https://docs.warden.dev/environments/types.html#wordpress) 

I personaly use warden for all my projects even magento, So why not give it a try and see how it can simplify your development workflow?

