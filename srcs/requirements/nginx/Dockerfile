FROM alpine:3.19

#install NGINX and OpenSSL
RUN apk update && apk upgrade && apk add --no-cache nginx openssl

#create the folder for SSL certificate
RUN mkdir -p /etc/nginx/ssl

# Generate the SSL certificate (self signed)
#strict requirement: TLSv1.2 or TLSv1.3
RUN openssl req -x509 -node -out /etc/nginx/ssl/inception.crt -keyout /etc/nginx/ssl/inception.key -subj "/C=FR/ST=IDF/L=Paris/0=42/OU=42/CN=login.42.fr/UID=login"

#create the folder to store NGINX conf files
RUN mkdir -p /var/run/nginx

COPY conf/nginx.conf /etc/nginx/http.d/default.conf

#Expose the only allowed port
EXPOSE 443

#Start NGINX in the foreground
CMD ["nginx", "-g", "deamon off;"]
