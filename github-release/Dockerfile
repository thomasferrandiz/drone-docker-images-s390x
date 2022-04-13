ARG GO_IMAGE=rancher/hardened-build-base:v1.16.9b7

FROM ${GO_IMAGE} as build
ARG upstream=https://github.com/drone-plugins/drone-github-release
ARG version=v1.0.0

WORKDIR /src
RUN git clone --depth=1 --branch=${version} ${upstream} .
RUN GOOS=linux GOARCH=s390x CGO_ENABLED=0 GO111MODULE=on go build -v -a -tags netgo -o release/linux/s390x/drone-github-release

FROM scratch
COPY --from=build /src/release/linux/s390x/drone-github-release /bin/
ENTRYPOINT [ "/bin/drone-github-release" ]
