FROM jetty:9.3-jre8

MAINTAINER Lidarr <lidarrdevelopment@gmail.com>

ENV SEARCH_HOME=/home/search
ENV INDEXES_VERSION=1
ENV RSYNC_PASSWORD=search
ENV SERVICE_8080_NAME=search-server
ENV SERVICE_8080_CHECK_TCP=true
ENV SERVICE_8080_CHECK_INTERVAL=15s
ENV SERVICE_8080_CHECK_TIMEOUT=3s

USER root

RUN apt-get update && apt-get install -y --no-install-recommends \
        bsdmainutils \
        psmisc \
        python \
        rsync \
        runit

COPY root /
RUN ln -sf /etc/sv/server /etc/service/

# Install consul
RUN install_consul_template.sh && \
        rm -f /usr/local/bin/install_consul_template.sh && \
        rm -f /usr/local/bin/install_runit.sh

# Install the war file
RUN curl -o $JETTY_HOME/webapps/ROOT.war ftp://data.musicbrainz.org/pub/musicbrainz/search/servlet/searchserver.war 

ENTRYPOINT ["/usr/local/bin/runsvinit"]
