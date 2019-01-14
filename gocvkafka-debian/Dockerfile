FROM adaickalavan/gocv-debian

#Author label
LABEL Author Adaickalavan Meiyappan

#Install dev tools for building Librdkafka and confluent-kafka-go
RUN apt-get update && apt-get install bash ca-certificates tar git openssl coreutils librdkafka-dev -y

# RUN apt-get -y update \
#         && apt-get install -y --no-install-recommends upx-ucl zip \
#         && apt-get clean \
#         && rm -rf /var/lib/apt/lists/*

# Build librdkafka
WORKDIR /root
RUN git clone https://github.com/edenhill/librdkafka.git
WORKDIR /root/librdkafka
RUN /root/librdkafka/configure
RUN make
RUN make install

# For golang applications
RUN mkdir /lib64 && ln -s /lib/libc.musl-x86_64.so.1 /lib64/ld-linux-x86-64.so.2

# ENV LIBRDKAFKA_VERSION 1.0.0

# RUN curl -Lk -o /root/librdkafka-${LIBRDKAFKA_VERSION}.tar.gz https://github.com/edenhill/librdkafka/archive/v${LIBRDKAFKA_VERSION}.tar.gz && \
#       tar -xzf /root/librdkafka-${LIBRDKAFKA_VERSION}.tar.gz -C /root && \
#       cd /root/librdkafka-${LIBRDKAFKA_VERSION} && \
#       ./configure --prefix /usr && make && make install && make clean && ./configure --clean

# Get confluent-kafka-go/kafka library
RUN go get -u github.com/confluentinc/confluent-kafka-go/kafka

# To verify that the Docker image has been built correctly, do the following.
# By enabling the ENTRYPOINT command below, running 
# ```
# docker run <image_name>
# ```
#
# should print the following message:
#
# ```
#gocv version: 0.18.0
#opencv lib version 4.0.0
# ```

# Run the app command by default when the container starts
# ENTRYPOINT ["go", "run", "$GOPATH/src/gocv.io/x/gocv/cmd/version/main.go"]
