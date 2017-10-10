FROM debian:stretch-slim@sha256:b4c6e46603728bdc550c9075be78439c45a0d509008770ad3775d097f28b6cca

ENV FILEBEAT_VERSION="6.0.0-rc1"
ENV FILEBEAT_SHA512="89cb8a510ecf876d707b803cacef3bc6fd4f536f706d2ef7280d65413a7c9cc65cd0941d2c4eb85a5ba3c01a4718da99bb3c911357a59086819ddb750eb25e2a"

RUN set -ex; \
  runDeps=''; \
  buildDeps='curl ca-certificates'; \
  export DEBIAN_FRONTEND=noninteractive; \
  apt-get update && apt-get install -y $runDeps $buildDeps --no-install-recommends; \
  \
  curl -SLs -o filebeat.tgz https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-${FILEBEAT_VERSION}-linux-x86_64.tar.gz; \
  echo "${FILEBEAT_SHA512}  filebeat.tgz" | sha512sum -c; \
  mkdir /opt/filebeat; \
  tar -xvzf filebeat.tgz --strip-components=1 -C /opt/filebeat; \
  ln -s /opt/filebeat/filebeat /usr/local/bin/filebeat; \
  filebeat version; \
  \
  apt-get purge -y --auto-remove $buildDeps; \
  rm -rf /var/lib/apt/lists/*; \
  rm -rf /var/log/dpkg.log /var/log/alternatives.log /var/log/apt
