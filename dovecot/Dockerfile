FROM debian:latest

RUN apt update && apt install -y \
    dovecot-core \
    dovecot-imapd


COPY files/dovecot.conf /etc/dovecot/dovecot.conf
COPY files/10-mail.conf /etc/dovecot/conf.d/10-mail.conf
COPY files/10-auth.conf /etc/dovecot/conf.d/10-auth.conf

RUN useradd -m -d /home/mengano -p '$1$74DwVVAy$6FwmhPYyVGeKB999en7I61' mengano && \
    useradd -m -d /home/fulano -p '$1$8mn2mnKJ$axLiAO6ocmx2fT9MR1DSF1' fulano && \
    mkdir -p /home/mengano/Maildir /home/fulano/Maildir && \  
    chown -R mengano:mengano /home/mengano && \  
    chown -R fulano:fulano /home/fulano && \
    chmod -R 700 /home/mengano /home/fulano  

EXPOSE 143
CMD ["dovecot", "-F"]