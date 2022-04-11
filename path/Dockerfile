FROM golang:1.17.5-alpine3.15 AS build
RUN apk add --no-cache git ca-certificates
ARG upstream=https://github.com/meltwater/drone-convert-pathschanged
ARG version=v0.6.0

WORKDIR /src
RUN git clone --depth=1 --branch=${version} ${upstream} .
RUN GOOS=linux GOARCH=s390x CGO_ENABLED=0 GO111MODULE=on go build -v -a -tags netgo -o release/linux/s390x/drone-convert-pathschanged

FROM scratch
EXPOSE 3000

ENV GODEBUG netdns=go

COPY --from=build /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/
COPY --from=build /src/release/linux/s390x/drone-convert-pathschanged /usr/local/bin/ 
ENTRYPOINT ["/usr/local/bin/drone-convert-pathschanged"]
