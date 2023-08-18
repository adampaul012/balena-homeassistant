FROM python:3.8-alpine

RUN apk add gcc linux-headers

COPY config.yml /config/config.yml

RUN pip install mqtt_io OPi.GPIO

RUN rm /usr/local/lib/python3.8/site-packages/mqtt_io/modules/gpio/orangepi.py

COPY orangepi.py /usr/local/lib/python3.8/site-packages/mqtt_io/modules/gpio/orangepi.py

CMD [ "python", "-m", "mqtt_io", "/config/config.yml" ]