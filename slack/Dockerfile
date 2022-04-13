ARG GO_IMAGE=rancher/hardened-build-base:v1.16.9b7

FROM ${GO_IMAGE} AS build
ARG upstream=https://github.com/drone-plugins/drone-slack
ARG version=v1.4.1

WORKDIR /src
RUN git clone --depth=1 --branch=${version} ${upstream} .
RUN GOOS=linux GOARCH=s390x CGO_ENABLED=0 GO111MODULE=on go build -v -a -tags netgo -o release/linux/s390x/drone-slack

FROM scratch
COPY --from=build /src/release/linux/s390x/drone-slack /usr/local/bin/
ENTRYPOINT ["/usr/local/bin/drone-slack"]
