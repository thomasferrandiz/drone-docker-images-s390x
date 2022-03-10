FROM golang:1.17.5-alpine3.15 AS build
RUN apk add --no-cache git
ARG upstream=https://github.com/drone-plugins/drone-github-release
ARG version=v1.0.0

WORKDIR /src
RUN git clone --depth=1 --branch=${version} ${upstream} .
RUN GOOS=linux GOARCH=s390x CGO_ENABLED=0 GO111MODULE=on go build -v -a -tags netgo -o release/linux/s390x/drone-github-release

FROM plugins/base:multiarch@sha256:3511e8151bedc65bae396cd3e93ba6662a593c60262d4d29958e58b3c4b2eb4a

COPY --from=build /src/release/linux/s390x/drone-github-release /bin/
ENTRYPOINT [ "/bin/drone-github-release" ]
