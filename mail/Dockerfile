FROM debian:latest

RUN apt update && apt install -y \
    postfix \
    cron \
    dovecot-core \
    dovecot-imapd \
    nano

COPY postfix/main.cfg /etc/postfix/main.cfg

CMD [ "cron", "-f" ]