# https://hub.docker.com/r/tarantool/tarantool/tags?page=1&name=2.&ordering=last_updated
FROM tarantool/tarantool:2.10.0-beta2 AS base
ENV ROCKS_INSTALLER 'tarantoolctl rocks'
# cmake make to build 'errors'
# https://pkgs.alpinelinux.org/packages?name=make&branch=v3.9&repo=main&arch=x86_64
RUN apk --no-cache add cmake=3.13.0-r0 make=4.2.1-r2
RUN set -x \
    && ${ROCKS_INSTALLER} install config \
    && ${ROCKS_INSTALLER} install errors

# https://hub.docker.com/_/alpine?tab=tags&ordering=last_updated
FROM alpine:3.15.0 AS alpine
RUN apk add --update --no-cache ca-certificates tzdata


# https://hub.docker.com/r/skillc0der/tarantool/
FROM scratch AS tarantool
COPY --from=alpine /usr/share/zoneinfo /usr/share/zoneinfo
COPY --from=alpine /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/
COPY --from=base \
  /etc/passwd \
  /etc/group \
 /etc/
COPY --from=base \
  /usr/lib/libicui18n.so.62 \
  /usr/lib/libicuuc.so.62 \
  /usr/lib/libreadline.so.7 \
  /usr/lib/libgomp.so.1 \
  /usr/lib/libgcc_s.so.1 \
  /usr/lib/libunwind-x86_64.so.8 \
  /usr/lib/libunwind.so.8 \
  /usr/lib/libstdc++.so.6 \
  /usr/lib/libicudata.so.62 \
  /usr/lib/libncursesw.so.6 \
 /usr/lib/
COPY --from=base \
  /usr/local/bin/tarantool-entrypoint.lua \
  /usr/local/bin/tarantool_set_config.lua \
  /usr/local/bin/docker-entrypoint.sh \
  /usr/local/bin/console \
  /usr/local/bin/tarantool_is_up \
  /usr/local/bin/tarantool \
 /usr/local/bin/
COPY --from=base /.rocks/lib/tarantool/ /.rocks/lib/tarantool/
COPY --from=base /.rocks/share/tarantool/ /.rocks/share/tarantool/
COPY --from=base /opt/tarantool/.rocks/share/tarantool/ /.rocks/share/tarantool/
COPY --from=base /usr/local/etc/default/tarantool /usr/local/etc/default/tarantool

#  volume containing operational data (snapshots, xlogs and vinyl runs)
COPY --from=base --chown=tarantool /var/lib/tarantool/ /var/lib/tarantool/


