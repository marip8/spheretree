FROM ubuntu:jammy

SHELL ["/bin/bash", "-c"]

ENV DEBIAN_FRONTEND noninteractive

USER root

RUN apt update -y -qq \
  && apt install git gcc g++ make -y -qq

ARG SPHERETREE_DIR=/opt/spheretree
RUN --mount=type=bind,target=${SPHERETREE_DIR},readwrite \
  cd ${SPHERETREE_DIR} \
  && ./configure \
  && make all AUTOCONF=: AUTOHEADER=: AUTOMAKE=: ACLOCAL=: \
  && cp src/makeTree* /opt

# Add the entrypoint
COPY docker/create_spheretree /usr/local/bin/create_spheretree
RUN chmod +x /usr/local/bin/create_spheretree
ENTRYPOINT ["/usr/local/bin/create_spheretree"]
