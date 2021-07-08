FROM ubuntu:focal
MAINTAINER Ajay Khanna <appliedstochastics@gmail.com>

# tzdata config from https://stackoverflow.com/a/47909037
ENV DEBIAN_FRONTEND noninteractive
ENV DEBCONF_NONINTERACTIVE_SEEN true

RUN apt-get update && \
    # Required build tools  
    apt-get install -y build-essential cmake && \
    # git to fetch the repo and wget to populate vendor
    apt-get install -y git wget && \
    # Clean up
    apt-get clean all && \
    rm -rf /var/lib/apt/lists/* && rm -rf /tmp/* && rm -rf /var/tmp/*

RUN cd / && \
    git clone https://github.com/genome/bam-readcount && \
    cd bam-readcount && \
    # For a specific tag enable the git checkout below
    #git checkout cram-v0.0.2 && \
    rm -rf build && \
    mkdir build && \
    cd build && \
    cmake .. && \
    make


FROM ubuntu:focal
ENV DEBIAN_FRONTEND noninteractive
ENV DEBCONF_NONINTERACTIVE_SEEN true

LABEL \
    description="Image supporting the bam-readcount program"

RUN apt-get update

RUN mkdir -p /opt/bam-readcount/bin
WORKDIR /opt/bam-readcount
COPY --from=0 /bam-readcount/build/bin/bam-readcount /opt/bam-readcount/bin/bam-readcount
RUN ln -s /opt/bam-readcount/bin/bam-readcount /usr/bin/bam-readcount
