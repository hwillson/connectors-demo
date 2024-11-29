FROM --platform=amd64 debian:bullseye-slim

WORKDIR /dist

# Make directory for config
RUN mkdir config

RUN apt-get update
RUN apt-get -y install \
    ca-certificates

# Clean up apt lists
RUN rm -rf /var/lib/apt/lists/*

# Copy and extract the router binary
ARG TARBALL=router-v2.0.0-preview.1-x86_64-unknown-linux-gnu.tar.gz

COPY ${TARBALL} ..
RUN tar --strip-components=1 -xzf ../${TARBALL}

LABEL org.opencontainers.image.authors="Apollo Graph, Inc. https://github.com/apollographql/router"
LABEL org.opencontainers.image.source="https://github.com/apollographql/router"

ENV APOLLO_ROUTER_CONFIG_PATH="/dist/config/router.yml"

# Create a wrapper script to run the router, use exec to ensure signals are handled correctly
RUN \
    echo '#!/usr/bin/env bash \
    \nset -e \
    \n \
    \n  exec /dist/router "$@" \
    \nfi \
    ' > /dist/router_wrapper.sh

# Make sure we can run our wrapper
RUN chmod 755 /dist/router_wrapper.sh

# Set labels for our image
LABEL org.opencontainers.image.authors="Apollo Graph, Inc. https://github.com/apollographql/router"
LABEL org.opencontainers.image.source="https://github.com/apollographql/router"

# Default executable is the wrapper script
ENTRYPOINT ["/dist/router_wrapper.sh"]
