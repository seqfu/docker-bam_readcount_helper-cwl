FROM alpine:latest
MAINTAINER Ajay Khanna <appliedstochastics@gmail.com>

RUN apk --no-cache add cmake make g++ git

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


FROM alpine:latest

LABEL \
    description="Alpine image with bam-readcount"

RUN apk add g++

RUN mkdir -p /opt/bam-readcount/bin
WORKDIR /opt/bam-readcount
COPY --from=0 /bam-readcount/build/bin/bam-readcount /opt/bam-readcount/bin/bam-readcount
RUN ln -s /opt/bam-readcount/bin/bam-readcount /usr/bin/bam-readcount
