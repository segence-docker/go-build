FROM golang:1.24.4-alpine3.22 AS builder

ARG LIBRDKAFKA_VERSION=v2.10.1

ENV PATH="/go/bin:${PATH}"
ENV GO111MODULE=on
ENV CGO_ENABLED=1
ENV GOOS=linux

RUN apk --no-cache add ca-certificates=20241121-r2
RUN apk update && \
    apk upgrade && \
    apk --no-cache add pkgconf=2.4.3-r0 git=2.49.0-r0 bash=5.2.37-r0 build-base=0.5-r3 sudo=1.9.17_p1-r0 && \
    rm -rf /var/cache/apk/*


RUN git clone --depth 1 --branch ${LIBRDKAFKA_VERSION} https://github.com/confluentinc/librdkafka /tmp/librdkafka

WORKDIR /tmp/librdkafka
RUN ./configure --prefix /usr && make && make install

WORKDIR /go

RUN rm -rf /tmp/librdkafka