ARG BCI_IMAGE=registry.suse.com/bci/bci-base:latest

FROM ${BCI_IMAGE} as bci-build
RUN zypper update -y && \
    zypper install -y git ca-certificates && \
    zypper clean --all

ARG upstream=https://github.com/drone/drone-git
ARG version=v1.2.1

WORKDIR /src
RUN git clone --depth=1 --branch=${version} ${upstream} .
RUN ls -la /src/posix
RUN cp -r /src/posix/clone* /usr/local/bin/
RUN rm -rf *

ENTRYPOINT ["/usr/local/bin/clone"]
