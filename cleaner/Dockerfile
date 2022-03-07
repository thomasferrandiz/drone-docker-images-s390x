FROM golang:1.17.5-alpine3.15 AS build
RUN apk add --no-cache git
ARG upstream=https://github.com/drone/drone-gc
ARG version=v1.0.0

WORKDIR /src
RUN git clone --depth=1 --branch=${version} ${upstream} .
RUN GOOS=linux GOARCH=s390x CGO_ENABLED=0 GO111MODULE=on go build -o release/linux/s390x/drone-gc github.com/drone/drone-gc

FROM scratch
COPY --from=build /src/release/linux/s390x/drone-gc  /usr/local/bin/
ENTRYPOINT ["/usr/local/bin/drone-gc"]
