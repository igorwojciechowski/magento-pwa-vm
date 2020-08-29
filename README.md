# magento-vm-docker

A docker-based virtual machine for Magento-PWA application.

## Built with

* VirtualBox
* Vagrant
* Ansible
* Docker

## Docker containers

* nginx 1.18
* php-fpm 7.3
* node
* mysql 5.6
* redis 6.0

## Requirements

* Oracle VirtualBox
* Vagrant

## Setup

1. Run and provision the machine

    * Clone repository
        ```bash
        $ git clone https://github.com/igorwojciechowski/magento-vm-docker.git
        ``` 
    * Go to repository
        ```bash
        $ cd magento-vm-docker
        ```
    * Run machine with Vagrant
        ```bash
        $ vagrant up
        ```
2. Clone projects repositories
    * SSH to machine
        ```bash
        $ ssh magento@192.168.33.10
        ```
    * Clone Magento repository
        ```bash
        $ git clone <magento_repository> /var/www/magento23os/
        ```
    * Clone PWA repository
        ```bash
        $ git clone <pwa_repository> /var/www/storefront/
        ```
3. Run docker containers
    * Go to docker directory
        ```bash
        $ cd ~/docker
        ```
    * Run docker-compose
        ```bash
        $ docker-compose up -d --build
        ```

## To do

* Configure PWA storefront to use https
* Add xdebug to PHP container
* Add Elasticsearch container
