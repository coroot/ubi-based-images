FROM clickhouse/clickhouse-server:25.1.3 AS base

FROM registry.access.redhat.com/ubi9/ubi

LABEL name="clickhouse" \
      vendor="Coroot, Inc." \
      maintainer="Coroot, Inc." \
      version=25.1.3 \
      release="1" \
      summary="ClickHouse" \
      description="ClickHouse UBI-based image."

COPY LICENSE /licenses/LICENSE

COPY --from=base /etc/clickhouse-server /etc/clickhouse-server
COPY --from=base /etc/clickhouse-keeper /etc/clickhouse-keeper
COPY --from=base /etc/clickhouse-client /etc/clickhouse-client
COPY --from=base /usr/bin/clickhouse /usr/bin/clickhouse
COPY --from=base /entrypoint.sh /entrypoint.sh

RUN ln -s /usr/bin/clickhouse /usr/bin/clickhouse-server \
    && ln -s /usr/bin/clickhouse /usr/bin/clickhouse-keeper \
    && ln -s /usr/bin/clickhouse /usr/bin/clickhouse-client

RUN mkdir /var/lib/clickhouse /var/log/clickhouse-server /docker-entrypoint-initdb.d \
    && chown -R nobody:nobody /etc/clickhouse-* /var/lib/clickhouse /var/log/clickhouse-server /docker-entrypoint-initdb.d

USER 65534:65534
EXPOSE 9000 8123 9009
VOLUME "/var/lib/clickhouse"
ENV CLICKHOUSE_CONFIG=/etc/clickhouse-server/config.xml
ENV CLICKHOUSE_UID=nobody
ENV CLICKHOUSE_GID=nobody
ENTRYPOINT ["/entrypoint.sh"]
