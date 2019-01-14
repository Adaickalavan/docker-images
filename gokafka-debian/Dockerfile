FROM golang:latest

ENV LIBRDKAFKA_VERSION 1.0.0

#Install dev tools
RUN apt-get -y update \
        && apt-get install -y --no-install-recommends upx-ucl zip \
        && apt-get clean \
        && rm -rf /var/lib/apt/lists/*

# Build librdkafka
RUN curl -Lk -o /root/librdkafka-${LIBRDKAFKA_VERSION}.tar.gz https://github.com/edenhill/librdkafka/archive/v${LIBRDKAFKA_VERSION}.tar.gz && \
      tar -xzf /root/librdkafka-${LIBRDKAFKA_VERSION}.tar.gz -C /root && \
      cd /root/librdkafka-${LIBRDKAFKA_VERSION} && \
      ./configure --prefix /usr && make && make install && make clean && ./configure --clean

# Get confluent-kafka-go/kafka library
RUN go get -u github.com/confluentinc/confluent-kafka-go/kafka
