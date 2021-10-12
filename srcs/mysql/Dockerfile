
FROM alpine:latest

#RUN sed -i "s/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g" /etc/apk/repositories
#RUN apk add mysql mysql-client
RUN apk update && \
	apk add --no-cache mysql mysql-client

# bisogna creare directory prima di copiare my.cnf, altrimenti da errore
RUN	mkdir -p /run/mysqld

COPY my.cnf /etc/.
COPY mysql_init.sql wordpress.sql /
COPY setup.sh init_wordpress.sh /

RUN chmod +x /setup.sh

EXPOSE 3306

ENTRYPOINT ["sh","/setup.sh"]
#CMD ./setup.sh
