FROM debian:latest

RUN apt update && apt install -y \
    mailutils \
    dovecot-core \
    wget


RUN echo "postfix postfix/mailname string aula.izv" | debconf-set-selections
RUN echo "postfix postfix/main_mailer_type string 'localhost'" | debconf-set-selections

RUN apt-get install postfix -y

RUN useradd -m -d /home/mengano -p '$1$74DwVVAy$6FwmhPYyVGeKB999en7I61' mengano && \
    useradd -m -d /home/fulano -p '$1$8mn2mnKJ$axLiAO6ocmx2fT9MR1DSF1' fulano && \
    mkdir -p /home/mengano/Maildir /home/fulano/Maildir && \
    chown -R mengano:mengano /home/mengano && \
    chown -R fulano:fulano /home/fulano


COPY files/main.cf /etc/postfix/main.cf

RUN apt-get clean && rm -rf /var/lib/apt/lists/*

EXPOSE 25
CMD ["postfix", "start-fg"]