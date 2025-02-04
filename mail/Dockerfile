FROM debian:latest

# Install basic packages
RUN apt update && apt install -y \
    cron \
    dovecot-core \
    dovecot-imapd \
    nano \
    iproute2 \
    systemctl \
    mailutils \
    mutt \
    debconf \
    wget

# Set correct postfix parameters
RUN echo "postfix postfix/mailname string pumukydev.test" | debconf-set-selections
RUN echo "postfix postfix/main_mailer_type string 'localhost'" | debconf-set-selections

# Install postfix after configuring it
RUN apt-get install postfix -y

# Create logs
RUN touch /var/log/mail.log && chmod 666 /var/log/mail.log

# Create mengano (password: m) and fulano (password: f) users
RUN useradd -m -p '$1$74DwVVAy$6FwmhPYyVGeKB999en7I61' mengano && \
    useradd -m -p '$1$8mn2mnKJ$axLiAO6ocmx2fT9MR1DSF1' fulano

# Copy configuration files
COPY postfix/main.cf /etc/postfix/main.cf
COPY dovecot/dovecot.conf /etc/dovecot/dovecot.conf
COPY dovecot/10-mail.conf /etc/dovecot/conf.d/10-mail.conf
COPY dovecot/10-auth.conf /etc/dovecot/conf.d/10-auth.conf

# Set correct permissions
RUN chmod 644 /etc/postfix/main.cf && \
    chmod 644 /etc/dovecot/dovecot.conf && \
    chmod 644 /etc/dovecot/conf.d/10-mail.conf && \
    chmod 644 /etc/dovecot/conf.d/10-auth.conf

# Expose some ports
EXPOSE 25 143 587 993

# Create entrypoint
COPY entrypoint.sh /entrypoint.sh

RUN chmod +x /entrypoint.sh

ENTRYPOINT [ "/entrypoint.sh" ]
