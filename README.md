# Mail Server with SquirrelMail

![SquirrelMail logo](./assets/squirrelmail.png)

## Introduction

SquirrelMail is a webmail client that allows users to access their email via a web interface. This documentation describes how to deploy SquirrelMail using Docker with separate containers for the application, web server, and mail server.

## Squema

Look at this mermaid squema

```mermaid
flowchart TD

    subgraph Docker
        subgraph Nginx["Nginx (Container)"]
            SquirrelMail["SquirrelMail (Mail client)"]
        end

        PHP["PHP (Backend)"]

    subgraph Mail["Mail (Container)"]
        direction LR
        subgraph Postfix
            Fulano["Fulano (User)"]
            Mengano["Mengano (User)"]
        end
        Dovecot["Dovecot (IMAP Server)"]
    end

    end

    subgraph Browser
        FulanoBrowser["Fulano (Browser)"]
        MenganoBrowser["Mengano (Browser)"]
    end

    PHP --> Nginx

    Nginx -->|Port 80 HTTP| FulanoBrowser
    Nginx -->|Port 80 HTTP| MenganoBrowser
    FulanoBrowser --> SquirrelMail
    MenganoBrowser --> SquirrelMail
    Dovecot -->|Port 143 IMAP| Postfix
    Postfix -->|Port 25 SMTP| Dovecot

    style Docker fill:transparent
    style Mail fill:transparent
    style Browser fill:transparent
    style Nginx fill:transparent
    style Postfix fill:transparent
```

## Setup Instructions

### Clone the Repository

```bash
   git clone https://github.com/PumukyDev/squirrelmail.git
   cd squirrelmail
```

### Deploy the servers

```bash
    docker-compose up -d --build
```

## Documentation
