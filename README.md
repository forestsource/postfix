# postfix
Postfix is a Mail Transport Agent (MTA).

## How to build the container on 25 port

```docker build --tag=docker.io/modularitycontainers/postfix .```

## How to use the container over standard 25 port

Command for running postfix docker container:

```
docker run -it -e MYHOSTNAME=localhost \
    -p 25:10025\
    -v /var/spool/postfix:/var/spool/postfix \
    -v /var/spool/mail:/var/spool/mail postfix
    -d docker.io/modularitycontainers/postfix
```

## How to use the container over standard TLS

Command for running postfix docker container:
```
docker run -it -e ENABLE_TLS -e DEBUG_MODE=yes -e MYHOSTNAME=localhost \
    -p 25:10025 \
    postfix -d docker.io/modularitycontainers/postfix
```

Environment variable DEBUG_MODE is used for debugging purposes
from postfix point of view.

## How to use the container with IMAP.

Command for running postfix docker container:
```
POSTFIX_CERTS_PATH=/etc/postfix/certs
docker run -it -e ENABLE_IMAP -e MYHOSTNAME=localhost
    -e DEBUG_MODE \
    -p 587:10587 \
    -v ${POSTFIX_CERTS_PATH}:/etc/postfix/certs \
    postfix -d docker.io/modularitycontainers/postfix
```
POSTFIX_CERTS_PATH contains certificates used by postfix, like self signed certificate, keys, etc.
Environment variable DEBUG_MODE is used for debugging purposes from postfix.

# How to generate self signed SSL certificate for postfix

In case, you enable TLS support for postfix, you need to have certificates for postfix service.

For more information about Postfix TLS support see `http://www.postfix.org/TLS_README.html`

The page `POSTFIX_CERTS_GENERATION.md` will help you with generation self signed certificate used by postfix.

## How to test the postfix mail server

See `help/help.md` file.
