FROM nginx:1.18.0-alpine

RUN apk update
RUN apk add bash

COPY ./etc/nginx/nginx.conf /etc/nginx/nginx.conf
COPY ./etc/nginx/sites-available/magento.conf /etc/nginx/sites-available/magento.conf
RUN mkdir /etc/nginx/sites-enabled/
RUN ln -s /etc/nginx/sites-available/magento.conf /etc/nginx/sites-enabled/magento.conf

RUN addgroup --gid 2222 magento
RUN adduser  magento --uid 2222  -G magento --disabled-password
RUN echo "magento:magento" | chpasswd

EXPOSE 80
EXPOSE 443

#CMD [ "nginx", "-c", "/etc/nginx/sites-available/magento.conf"]