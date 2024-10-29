FROM golang:1.23.2-alpine AS builder

ENV PATH="/go/bin:${PATH}"
ENV GO111MODULE=on
ENV CGO_ENABLED=1
ENV GOOS=linux

RUN apk --no-cache add ca-certificates=20240705-r0
RUN apk update && \
    apk upgrade && \
    apk --no-cache add pkgconf=2.2.0-r0 git=2.45.2-r0 bash=5.2.26-r0 build-base=0.5-r3 sudo=1.9.15_p5-r0 && \
    rm -rf /var/cache/apk/*


RUN git clone https://github.com/confluentinc/librdkafka /tmp/librdkafka

WORKDIR /tmp/librdkafka
RUN ./configure --prefix /usr && make && make install

WORKDIR /go

RUN rm -rf /tmp/librdkafka