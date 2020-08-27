FROM node:alpine3.11

USER root

RUN apk update
RUN apk add bash \
            python \
            python3 \
            curl \
            openssl \
            git \
            build-base \
            sudo

RUN echo "192.168.33.10 magento.backend" >> /etc/hosts

RUN addgroup --gid 2222 magento
RUN adduser  magento --uid 2222  -G magento --disabled-password
RUN echo "magento:magento" | chpasswd

# --- Add user to sudoers
RUN echo "magento ALL=(ALL) ALL" > /etc/sudoers.d/magento
RUN chmod 0440 /etc/sudoers.d/magento
RUN echo "Set disable_coredump false" >> /etc/sudo.conf

WORKDIR /var/www/storefront/