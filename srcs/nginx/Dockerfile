
# alpine è il sistema operativo che uso per il mio contenitore
# i comandi che eseguirò verranno eseguiti in quel contenitore
# sto usando delle risorse del computer per simulare un altro computer (questo è il contenitore)
FROM alpine:latest

# installo pacchetti necessari con apk (perche sono su alpine)
RUN apk update && \
	apk add --no-cache nginx openssh openssl

# sposto file dentro container
COPY nginx.conf index.html setup.sh ./

# Setup nginx
RUN mkdir -p /run/nginx www/html && \
	mv nginx.conf /etc/nginx/ && \
	mv index.html /www/html/

# creo e certifico una chiave ssl
RUN openssl req -x509 -nodes -days 365 -new -newkey rsa:2048 \
	-subj "/C=IT/ST=Italy/L=Rome/O=luiss/OU=42rome/CN=etaranti" \
	-keyout /etc/ssl/nginx-selfsigned.key -out /etc/ssl/nginx-selfsigned.crt
# /etc/ssl/certs/services.crt (cclaude)

# Setup SSH. ssh-keygen -A genera chiavi ssh
RUN ssh-keygen -A && \
	adduser -D user && \
	echo "user:password" | chpasswd


EXPOSE 22 80 443

CMD ./setup.sh

