FROM nginx:1.18.0-alpine

RUN apk update
RUN apk add bash \
            openssl

COPY ./etc/nginx/nginx.conf /etc/nginx/nginx.conf
COPY ./etc/nginx/sites-available/magento.conf /etc/nginx/sites-available/magento.conf
RUN mkdir /etc/nginx/sites-enabled/
RUN ln -s /etc/nginx/sites-available/magento.conf /etc/nginx/sites-enabled/magento.conf

RUN addgroup --gid 2222 magento
RUN adduser  magento --uid 2222  -G magento --disabled-password
RUN echo "magento:magento" | chpasswd


RUN mkdir -p /etc/ssl/certs/
RUN mkdir -p /etc/ssl/private/

RUN openssl req -x509 \
                -nodes \
                -days 365 \
                -newkey rsa:2048 \
                -keyout /etc/ssl/private/nginx-selfsigned.key \
                -out /etc/ssl/certs/nginx-selfsigned.crt \
                -subj "/CN=Magento/C=MA/ST=Magento/L=Magento/O=Magento/OU=Magento/"


EXPOSE 80
EXPOSE 443