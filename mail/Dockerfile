FROM debian:latest

RUN apt update && apt install -y \
    postfix \
    cron \
    dovecot-core \
    dovecot-imapd \
    dovecot-pop3d \
    nano \
    iproute2 \
    systemctl \
    wget

RUN touch /var/log/mail.log && chmod 666 /var/log/mail.log

# Copia configuraciones
COPY postfix/main.cfg /etc/postfix/main.cfg
#COPY dovecot/dovecot.conf /etc/dovecot/dovecot.conf
COPY dovecot/10-mail.conf /etc/dovecot/conf.d/10-mail.conf
COPY dovecot/10-auth.conf /etc/dovecot/conf.d/10-auth.conf
#COPY dovecot/10-master.conf /etc/dovecot/conf.d/10-master.conf

# Expone puertos
EXPOSE 25 143 587 993

# Inicia servicios
CMD service postfix start && service dovecot start && tail -f /var/log/mail.log

