FROM openjdk:8-jre-stretch

MAINTAINER Lidarr <lidarrdevelopment@gmail.com>

ENV SEARCH_HOME=/home/search
ENV INDEXES_VERSION=1
ENV SERVICE_873_NAME=search-indexer
ENV SERVICE_873_CHECK_TCP=true
ENV SERVICE_873_CHECK_INTERVAL=15s
ENV SERVICE_873_CHECK_TIMEOUT=3s
ENV SEARCH_SERVER_CHILL_TIME_BETWEEN_RUNS=86400

RUN apt-get update && apt-get install -y --no-install-recommends \
        ca-certificates \
        curl \
	python \
        rsync \
        runit

COPY root /
RUN ln -sf /etc/sv/indexer /etc/service/

# Install consul
RUN install_consul_template.sh && \
        rm -f /usr/local/bin/install_consul_template.sh && \
        rm -f /usr/local/bin/install_runit.sh

# Install the war file
RUN curl -o /home/search/index.jar ftp://data.musicbrainz.org/pub/musicbrainz/search/index/index.jar

EXPOSE 873
ENTRYPOINT ["/usr/local/bin/runsvinit"]
