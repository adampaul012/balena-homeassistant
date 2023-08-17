FROM python:3.9.13-alpine

RUN apk add py3-pip

RUN python -m pip3 install mqtt-io

COPY config.yml /config/config.yml

RUN python3 -m mqtt_io /config/config.yml