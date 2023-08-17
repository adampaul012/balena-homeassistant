FROM python:3.8-alpine

RUN apk update

RUN apk add py3-pip

RUN python -m pip install mqtt-io

COPY config.yml /config/config.yml

RUN python3 -m mqtt_io /config/config.yml