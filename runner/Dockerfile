ARG GO_IMAGE=rancher/hardened-build-base:v1.16.9b7
#ARG BCI_IMAGE=registry.suse.com/bci/bci-base:latest

ARG BCI_IMAGE=scratch

FROM ${GO_IMAGE} as build
ARG upstream=https://github.com/drone-runners/drone-runner-docker
ARG version=v1.6.3

WORKDIR /src
RUN git clone --depth=1 --branch=${version} ${upstream} .
RUN GOOS=linux GOARCH=s390x CGO_ENABLED=0 GO111MODULE=on go build -v -a -tags netgo -o release/linux/s390x/drone-runner-docker

FROM ${BCI_IMAGE}
COPY --from=build /src/release/linux/s390x/drone-runner-docker /usr/local/bin/
ENTRYPOINT ["/usr/local/bin/drone-runner-docker"]
