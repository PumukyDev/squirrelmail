FROM debian:latest

RUN apt update && apt install -y \
    postfix \
    cron \
    dovecot-core \
    dovecot-imapd \
    dovecot-pop3d \
    nano \
    iproute2 \
    systemctl

COPY postfix/main.cfg /etc/postfix/main.cfg

COPY dovecot/10-mail.conf /etc/dovecot/conf.d/10-mail.conf 
COPY dovecot/10-auth.conf /etc/dovecot/conf.d/10-auth.conf

CMD [ "cron", "-f" ]