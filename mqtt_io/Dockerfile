FROM python:3.8-alpine


RUN apk update

RUN apk add py3-pip py3-virtualenv cargo openssl-dev libffi-dev rust pyYAML==5.4.1

COPY config.yml /config/config.yml

RUN pip install --no-cache-dir wheel setuptools-rust && \
    if [ "${BUILDX_QEMU_ENV}" = "true" -a "$(getconf LONG_BIT)" = "32" ]; then \
        pip install --no-cache-dir cryptography==3.3.2; \
    fi && \
    pip install --no-cache-dir poetry

COPY pyproject.toml ./

RUN poetry export -o /requirements.txt && \
    mkdir -p /home/mqtt_io && \
    python -m venv /home/mqtt_io/venv && \
    /home/mqtt_io/venv/bin/pip install wheel

RUN useradd -m -s /bin/bash mqtt_io
USER mqtt_io
WORKDIR /home/mqtt_io

COPY --from=requirements --chown=mqtt_io /home/mqtt_io/venv ./venv
COPY --from=requirements /requirements.txt ./
RUN venv/bin/python -m pip install --upgrade pip
RUN venv/bin/pip install -r requirements.txt

COPY --chown=mqtt_io mqtt_io mqtt_io


CMD [ "venv/bin/python", "-m", "mqtt_io", "/config/config.yml" ]