FROM nginx:1.18.0-alpine

RUN apk update
RUN apk add bash \
            openssl

COPY ./etc/nginx/nginx.conf /etc/nginx/nginx.conf
COPY ./etc/nginx/sites-available/magento.conf /etc/nginx/sites-available/magento.conf
COPY ./etc/nginx/sites-available/storefront.conf /etc/nginx/sites-available/storefront.conf

RUN mkdir /etc/nginx/sites-enabled/
RUN ln -s /etc/nginx/sites-available/magento.conf /etc/nginx/sites-enabled/magento.conf
RUN ln -s /etc/nginx/sites-available/storefront.conf /etc/nginx/sites-enabled/storefront.conf

RUN addgroup --gid 2222 magento
RUN adduser  magento --uid 2222  -G magento --disabled-password
RUN echo "magento:magento" | chpasswd

RUN mkdir -p /etc/ssl/certs/
RUN mkdir -p /etc/ssl/private/

# --- Generate self-signed certificate for backend domain
RUN openssl req -x509 \
                -nodes \
                -days 365 \
                -newkey rsa:2048 \
                -keyout /etc/ssl/private/magento.backend.key \
                -out /etc/ssl/certs/magento.backend.crt \
                -subj "/CN=Magento/C=MA/ST=Magento/L=Magento/O=Magento/OU=Magento/"

# --- Generate self-signed certificate for frontend domain
RUN openssl req -x509 \
                -nodes \
                -days 365 \
                -newkey rsa:2048 \
                -keyout /etc/ssl/private/magento.frontend.key \
                -out /etc/ssl/certs/magento.frontend.crt \
                -subj "/CN=Magento/C=MA/ST=Magento/L=Magento/O=Magento/OU=Magento/"

EXPOSE 80
EXPOSE 443