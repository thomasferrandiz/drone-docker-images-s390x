ARG GO_IMAGE=rancher/hardened-build-base:v1.16.9b7

FROM ${GO_IMAGE} AS build
ARG upstream=https://github.com/drone/drone-gc
ARG version=v1.0.0

WORKDIR /src
RUN git clone --depth=1 --branch=${version} ${upstream} .
RUN GOOS=linux GOARCH=s390x CGO_ENABLED=0 GO111MODULE=on go build -o release/linux/s390x/drone-gc github.com/drone/drone-gc

FROM scratch
COPY --from=build /src/release/linux/s390x/drone-gc  /usr/local/bin/
ENTRYPOINT ["/usr/local/bin/drone-gc"]
