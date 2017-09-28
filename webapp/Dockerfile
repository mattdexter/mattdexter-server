FROM python:3-alpine

# Initialize
RUN mkdir -p /data/webapp
WORKDIR /data/webapp
COPY requirements.txt /data/webapp/

# Setup
RUN apk update
RUN apk upgrade

RUN apk add --update \
    python3 python3-dev postgresql-client \
    postgresql-dev build-base gettext

RUN pip3 install --upgrade pip
RUN pip3 install gunicorn
RUN pip3 install -r requirements.txt

# Clean
RUN apk del -r python3-dev postgresql

# Prepare
COPY . /data/webapp
COPY ./entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

ENTRYPOINT ["/bin/sh", "/entrypoint.sh"]