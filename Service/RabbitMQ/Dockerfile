FROM rabbitmq:3.9.16-management

LABEL maintainer="KycKyc" version="3.9.16-2.0.0"

RUN rabbitmq-plugins enable --offline rabbitmq_federation_management

# Setup UTF-8
ENV TERM=xterm
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get clean && apt-get update && apt-get install -y --no-install-recommends apt-utils && apt-get install -y locales && locale-gen en_US.UTF-8 && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

COPY --chown=rabbitmq:rabbitmq configs/rabbitmq.conf /etc/rabbitmq/rabbitmq.conf