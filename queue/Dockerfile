# Based on scratch image
FROM skillc0der/tarantool:2.10.0-beta2-scratch as base


# Special image to using with queue module
# https://github.com/tarantool/queue
FROM scratch AS queue
COPY --from=base /usr/lib/ /usr/lib/
COPY --from=base /usr/local/bin/ /usr/local/bin/
COPY --from=base \
  /.rocks/lib/tarantool/lfs.so \
 /.rocks/lib/tarantool/
 COPY --from=base \
  /.rocks/share/tarantool/config.lua \
 /.rocks/share/tarantool/
COPY --from=base /etc/ /etc/
COPY --from=base /usr/share/zoneinfo /usr/share/zoneinfo
COPY --from=base /.rocks/lib/tarantool/http/ /.rocks/lib/tarantool/http/
COPY --from=base /.rocks/share/tarantool/queue/ /.rocks/share/tarantool/queue/
#  volume containing operational data (snapshots, xlogs and vinyl runs)
COPY --from=base --chown=tarantool /var/lib/tarantool/ /var/lib/tarantool/

