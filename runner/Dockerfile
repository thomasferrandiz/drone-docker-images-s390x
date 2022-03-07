FROM golang:1.17.5-alpine3.15 AS build
RUN apk add --no-cache git
ARG upstream=https://github.com/drone-runners/drone-runner-docker
ARG version=v1.6.3

WORKDIR /src
RUN git clone --depth=1 --branch=${version} ${upstream} .
RUN GOOS=linux GOARCH=s390x CGO_ENABLED=0 GO111MODULE=on go build -v -a -tags netgo -o release/linux/s390x/drone-runner-docker

FROM scratch
COPY --from=build /src/release/linux/s390x/drone-runner-docker /usr/local/bin/
ENTRYPOINT ["/usr/local/bin/drone-runner-docker"]
