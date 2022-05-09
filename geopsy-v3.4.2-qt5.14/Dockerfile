FROM rabits/qt:5.14-desktop

LABEL IMAGE_NAME="jpvantassel/geospy-docker:3.4.2-qt5.14"
LABEL MAINTAINER="Joseph P. Vantassel <joseph.p.vantassel@gmail.com>"

COPY geopsypack-src-3.4.2.tar.gz /home/user/

RUN sudo apt update \
 && sudo apt upgrade --yes \
 && sudo apt install --yes --quiet --no-install-recommends \
    g++ \
    gfortran \
    libfftw3-dev \
    liblapack-dev \
    zlib1g-dev \
    libopenblas-dev \
 && sudo apt clean

RUN /bin/bash -c \
    cd /home/user \
 && tar -xf geopsypack-src-3.4.2.tar.gz \
 && rm geopsypack-src-3.4.2.tar.gz \
 && mkdir geopsy \
 && cd geopsypack-src-3.4.2 \
 && ./configure -prefix /home/user/geopsy/ -march native --accept-license \
 && make \
 && sudo make install \
 && cd /home/user/ \
 && rm -rf geopsypack-src-3.4.2

ENV PATH=/home/user/geopsy/bin/:$PATH

RUN sudo apt update \
 && sudo apt upgrade --yes \
 && sudo apt install --yes --quiet --no-install-recommends \
    python3 \
    python3-pip \
 && sudo apt clean
