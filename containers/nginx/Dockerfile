FROM nginx:alpine

COPY ./conf.d/ /etc/nginx/conf.d/

RUN mkdir -p /etc/nginx/include.d/
COPY ./include.d/ /etc/nginx/include.d/

RUN mkdir -p /var/www/

RUN apk --update --no-cache add openssl

WORKDIR /etc/ssl/localhost/
RUN \
  openssl genrsa 2048 > localhost.key && \
  openssl req -new -key localhost.key -subj "/C=JP/ST=Tokyo/L=Chuo-ku/O=RMP Inc./OU=web/CN=localhost" > localhost.csr && \
  openssl x509 -in localhost.csr -days 3650 -req -signkey localhost.key > localhost.crt

WORKDIR /etc/ssl/
RUN \
  openssl dhparam 1024 > dhparam.key && \
  openssl rand 48 > ssl_session_ticket.key

RUN \
  chmod 755 -R /var/www/ && \
  chmod 400 /etc/ssl/localhost/localhost.key

WORKDIR /var/www/
