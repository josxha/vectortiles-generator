FROM golang:bookworm

# Install imposm3
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
      libprotobuf-dev \
      libleveldb-dev \
      libgeos-dev \
      postgresql-client \
      wget \
      --no-install-recommends \

RUN go get github.com/omniscale/imposm3 \
 && go install github.com/omniscale/imposm3 \
 && apt-get purge -y --auto-remove \
    g++ gcc libc6-dev make git \
 && rm -rf /var/lib/apt/lists/*

ENV IMPORT_DATA_DIR=/import \
    IMPOSM_CACHE_DIR=/cache \
    MAPPING_YAML=/usr/src/app/mapping.yml

WORKDIR /usr/src/app
COPY . /usr/src/app/

CMD ["./import-pbf.sh"]
