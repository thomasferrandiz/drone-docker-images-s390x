FROM golang:1.17.5-alpine AS build
RUN apk add --no-cache git
ARG upstream=https://github.com/drone/drone-git
ARG version=v1.2.1

WORKDIR /src
RUN git clone --depth=1 --branch=${version} ${upstream} .

FROM alpine:3.15.0
RUN apk add --no-cache ca-certificates git git-lfs openssh curl perl aws-cli sudo
COPY --from=build /src/posix /usr/local/bin/
ENTRYPOINT ["/usr/local/bin/clone"]

