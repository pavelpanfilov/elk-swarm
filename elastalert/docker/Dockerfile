FROM python:3.6-slim-buster

LABEL maintainer="Pavel Panfilov"
# forked from https://github.com/krizsan/elastalert-docker

ENV SET_CONTAINER_TIMEZONE False
ENV CONTAINER_TIMEZONE Europe/Moscow
ENV CONFIG_DIR /opt/config
ENV RULES_DIRECTORY /opt/rules
ENV ELASTALERT_CONFIG ${CONFIG_DIR}/elastalert_config.yaml
ENV LOG_DIR /opt/logs
ENV ELASTALERT_HOME /opt/elastalert
ENV ELASTALERT_SUPERVISOR_CONF ${CONFIG_DIR}/elastalert_supervisord.conf
ENV ELASTICSEARCH_HOST elasticsearchhost
ENV ELASTICSEARCH_PORT 9200
ENV ELASTICSEARCH_TLS False
ENV ELASTICSEARCH_TLS_VERIFY False
ENV ELASTALERT_INDEX elastalert_status

RUN apt-get update && \
    apt-get install -y gcc ca-certificates openntpd wget libmagic-dev && \
    mkdir -p "${ELASTALERT_HOME}"

WORKDIR /opt/elastalert

RUN pip install elastalert==0.2.1 && \
    pip uninstall python-magic --yes && \
    pip install python-magic-debian-bin && \
    pip install supervisor && \
    mkdir -p "${CONFIG_DIR}" && \
    mkdir -p "${RULES_DIRECTORY}" && \
    mkdir -p "${LOG_DIR}" && \
    mkdir -p /var/empty && \
    apt-get remove -y --purge gcc && \
    apt-get clean autoclean && \
    apt-get autoremove --yes && \
    rm -rf /var/lib/{apt,dpkg,cache,log}/

COPY ./start-elastalert.sh /opt/
COPY ./config.yaml.example "${ELASTALERT_HOME}"
COPY ./supervisord.conf.example "${ELASTALERT_HOME}"

RUN chmod +x /opt/start-elastalert.sh

CMD ["/opt/start-elastalert.sh"]