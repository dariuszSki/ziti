# this builds docker.io/openziti/ziti-cli
FROM registry.access.redhat.com/ubi8/ubi-minimal
# This build stage grabs artifacts that are copied into the final image.
# It uses the same base as the final image to maximize docker cache hits.

ARG ARTIFACTS_DIR=./release
ARG DOCKER_BUILD_DIR=.
# e.g. linux
ARG TARGETOS
# e.g. arm64
ARG TARGETARCH

### Required OpenShift Labels 
LABEL name="openziti/ziti-cli" \
      maintainer="developers@openziti.org" \
      vendor="NetFoundry" \
      summary="Run the OpenZiti CLI" \
      description="Run the OpenZiti CLI"

USER root

### add licenses to this directory
RUN mkdir -m0755 /licenses
COPY ./LICENSE /licenses/apache.txt

RUN mkdir -p /usr/local/bin
COPY ${ARTIFACTS_DIR}/${TARGETARCH}/${TARGETOS}/ziti /usr/local/bin/
RUN chmod 0755 /usr/local/bin/ziti

COPY ${DOCKER_BUILD_DIR}/entrypoint.sh /
RUN chmod +x /entrypoint.sh
USER nobody
ENTRYPOINT [ "/entrypoint.sh" ]
CMD [ "ziti" ]
