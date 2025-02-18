FROM python:3.7.3-alpine3.9

# runtime dependencies
RUN set -ex \
	&& apk add --no-cache --virtual .pgadmin4-rundeps \
		libffi-dev \
		bash \
		postgresql

ENV PGADMIN4_VERSION 4.9
ENV PGADMIN4_DOWNLOAD_URL https://ftp.postgresql.org/pub/pgadmin/pgadmin4/v4.9/pip/pgadmin4-4.9-py2.py3-none-any.whl

# Metadata
LABEL org.label-schema.name="pgAdmin4" \
      org.label-schema.version="$PGADMIN4_VERSION" \
      org.label-schema.license="PostgreSQL" \
      org.label-schema.url="https://www.pgadmin.org" \
      org.label-schema.vcs-url="https://github.com/fenglc/dockercloud-pgAdmin4"

RUN set -ex \
	&& apk add --no-cache --virtual .build-deps \
		make \
		libffi-dev \
		gcc \
		musl-dev \
		postgresql-dev \
	&& pip --no-cache-dir install \
		$PGADMIN4_DOWNLOAD_URL \
	&& apk del .build-deps

VOLUME /var/lib/pgadmin

COPY docker-entrypoint.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/docker-entrypoint.sh
ENTRYPOINT ["docker-entrypoint.sh"]

EXPOSE 5050
CMD ["pgadmin4"]
