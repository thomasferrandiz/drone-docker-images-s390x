FROM golang:1.17.5-alpine3.15 AS build
RUN apk add --no-cache git
ARG upstream=https://github.com/drone-plugins/drone-docker
ARG version=v20.11.0

WORKDIR /src
RUN git clone --depth=1 --branch=${version} ${upstream} .
RUN GOOS=linux GOARCH=s390x CGO_ENABLED=0 GO111MODULE=on go build -v -a -tags netgo -o release/linux/s390x/drone-docker ./cmd/drone-docker

FROM s390x/docker:dind

ENV DOCKER_HOST=unix:///var/run/docker.sock
COPY --from=build /src/release/linux/s390x/drone-docker /bin/
ENTRYPOINT ["/usr/local/bin/dockerd-entrypoint.sh", "/bin/drone-docker"]
