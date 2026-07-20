FROM docker.io/falcosecurity/falco-driver-loader:0.44.1

# Ubuntu 26.04's Linux 7.0 kernel is built with GCC 15 and uses compiler
# options that the upstream loader image's GCC 12 cannot understand.
RUN echo "deb http://deb.debian.org/debian sid main" > /etc/apt/sources.list.d/sid.list \
    && apt-get update \
    && apt-get install -y --no-install-recommends gcc-15 \
    && ln -sf /usr/bin/gcc-15 /usr/bin/gcc \
    && rm -rf /var/lib/apt/lists/* \
    && gcc --version
