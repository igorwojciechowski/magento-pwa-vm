FROM node:alpine3.11

USER root

RUN apk update
RUN apk add bash \
            python \
            python3 \
            curl \
            openssl \
            git

RUN echo "192.168.33.10     magento.backend" >> /etc/hosts

RUN addgroup --gid 2222 magento
RUN adduser  magento --uid 2222  -G magento --disabled-password
RUN echo "magento:magento" | chpasswd

WORKDIR /var/www/storefront/