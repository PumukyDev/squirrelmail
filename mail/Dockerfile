FROM debian:latest

RUN apt update && apt install -y \
    postfix \
    cron \
    dovecot-core \
    dovecot-imapd \
    nano

CMD [ "cron", "-f" ]