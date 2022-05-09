FROM ubuntu:xenial

LABEL IMAGE_NAME="jpvantassel/geospy-docker:2.10.1-qt4.8"
LABEL MAINTAINER="Joseph P. Vantassel <joseph.p.vantassel@gmail.com>"

RUN apt update \
 && apt upgrade --yes \
 && apt install --yes --quiet --no-install-recommends \
   build-essential \
   qt4-default \
   g++ \
   gfortran \
   libfftw3-dev \
   liblapack-dev \
   zlib1g-dev \
   libopenblas-dev \
   python3 \
   python3-pip \
 && apt clean

RUN mkdir -p /home/user

COPY geopsypack-src-2.10.1.tar.gz /home/user/

RUN cd /home/user/ \
 && tar -xf geopsypack-src-2.10.1.tar.gz \
 && rm geopsypack-src-2.10.1.tar.gz \
 && mkdir geopsy \
 && cd geopsypack-src-2.10.1 \
 && sed -i 's/LICENSE_ACCEPTED="no"/LICENSE_ACCEPTED="yes"/' configure \
 && ./configure -prefix /home/user/geopsy/ -I /home/user/geopsypack-src-2.10.1/include/ -L /home/user/geopsypack-src-2.10.1/lib/ -pch \
 && make -j 8 \
 && make install \
 && cd /home/user/ \
 && rm -rf geopsypack-src-2.10.1

ENV PATH=/home/user/geopsy/bin/:$PATH
