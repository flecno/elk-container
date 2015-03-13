FROM debian:wheezy

ENV KIBANA_PKG_NAME kibana-4.0.1-linux-x64
ENV DEBIAN_FRONTEND noninteractive

# install system requirements
RUN apt-get update \
    && apt-get -y --no-install-recommends install \
        wget \
        ca-certificates \
    && rm -rf /var/lib/apt/lists/*

# simple download the kibana package which bundles all needed binaris like nodejs
RUN wget -q -O /tmp/kibana.tar.gz https://download.elasticsearch.org/kibana/kibana/${KIBANA_PKG_NAME}.tar.gz \
		&& tar xfz /tmp/kibana.tar.gz -C /tmp \
		&& mv /tmp/${KIBANA_PKG_NAME} /kibana \
		&& rm -f /tmp/kibana.tar.gz

# start kibana server connected to the specified elasticsearch
# the environment variables filled by dockers [container linking](https://docs.docker.com/userguide/dockerlinks/)
CMD /kibana/bin/kibana \
	--elasticsearch "http://${ELASTICSEARCH_PORT_9200_TCP_ADDR}:${ELASTICSEARCH_PORT_9200_TCP_PORT}"

EXPOSE 5601

