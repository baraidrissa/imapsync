## Dockerfile for building a docker imapsync image

# $Id: Dockerfile,v 1.43 2022/05/17 14:29:36 gilles Exp gilles $
# I use the following command to build the image:
#
#  docker build -t gilleslamiral/imapsync . 
#
# where this Dockerfile is in the current directory
# 
# This Dockerfile build an image with two imapsync
# 1) One comes from https://imapsync.lamiral.info/imapsync
#    and goes to /usr/bin/imapsync in the Docker image
#    It is used with the command:
#
#    docker run gilleslamiral/imapsync imapsync ...
# 
# 2) One comes from the local file ./imapsync
#    and goes to /imapsync in the Docker image
#    It is used with the command:
#
#    docker run gilleslamiral/imapsync /imapsync ...


# I thank you very much
# I like thanks
# I like stars
# I like money to keep on doing this stuff

# Number of imapsync images pulled so far (2022_04_04): 673551
# Command used:
# curl -s https://hub.docker.com/v2/repositories/gilleslamiral/imapsync/ | jq '.pull_count'

# Debian Bullseye is Debian 11

FROM debian:bullseye 

LABEL   maintainer="Gilles LAMIRAL <gilles@lamiral.info>" \
        description="Imapsync" \
        documentation="https://imapsync.lamiral.info/#doc"

# I put a copy of the Dockerfile in the image itself
# It can help maintenance, isn't it?
# Also put optionally my local and usually more recent imapsync on /, for testing purpose

COPY Dockerfile imapsyn[c] prerequisites_imapsyn[c] /

RUN set -xe && \
  apt-get update \
  && apt-get install -y \
  libauthen-ntlm-perl \
  libcgi-pm-perl \
  libcrypt-openssl-rsa-perl \
  libcrypt-openssl-pkcs12-perl \
  libdata-uniqid-perl \
  libencode-imaputf7-perl \
  libfile-copy-recursive-perl \
  libfile-tail-perl \
  libio-compress-perl \
  libio-socket-ssl-perl \
  libio-socket-inet6-perl \
  libio-tee-perl \
  libhtml-parser-perl \
  libjson-webtoken-perl \
  libmail-imapclient-perl \
  libparse-recdescent-perl \
  libmodule-scandeps-perl \
  libpar-packer-perl \
  libproc-processtable-perl \
  libreadonly-perl \
  libregexp-common-perl \
  libsys-meminfo-perl \
  libterm-readkey-perl \
  libtest-mockobject-perl \
  libtest-pod-perl \
  libunicode-string-perl \
  liburi-perl  \
  libwww-perl \
  procps \
  wget \
  make \
  cpanminus \
  lsof \
  ncat \
  openssl \
  ca-certificates \
  && rm -rf /var/lib/apt/lists/* \
  && cpanm IO::Socket::SSL

# I added the IO::Socket::SSL update to avoid the annoying, confusing and useless warning
# DEBUG: .../IO/Socket/SSL.pm:1177: global error: Undefined SSL object

RUN set -xe \
  && cd /usr/bin/ \
  && pwd \
  && wget -N --no-check-certificate https://imapsync.lamiral.info/imapsync \
        https://imapsync.lamiral.info/prerequisites_imapsync \
        https://raw.githubusercontent.com/google/gmail-oauth2-tools/master/python/oauth2.py \
  && chmod +x imapsync oauth2.py \
  && /usr/bin/imapsync --testslive && /usr/bin/imapsync --tests # just_a_comment_to_force_update 2022_04_04_21_16_50

USER nobody:nogroup

ENV HOME /var/tmp/

WORKDIR /var/tmp/

STOPSIGNAL SIGINT

CMD ["/usr/bin/imapsync"]

# 
# End of imapsync Dockerfile 

