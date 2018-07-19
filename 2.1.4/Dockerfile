FROM geographica/gdal2:2.3.1

MAINTAINER shun-tak <shun.tak221@gmail.com>

ENV OSMCOASTLINE_VERSION 2.1.4
ENV PROTOZERO_VERSION 1.6.2
ENV LIBOSMIUM_VERSION 2.14.0

WORKDIR /usr/local/src

ADD https://github.com/osmcode/osmcoastline/archive/v${OSMCOASTLINE_VERSION}.tar.gz osmcoastline-${OSMCOASTLINE_VERSION}.tar.gz
ADD https://github.com/mapbox/protozero/archive/v${PROTOZERO_VERSION}.tar.gz protozero-${PROTOZERO_VERSION}.tar.gz
ADD https://github.com/osmcode/libosmium/archive/v${LIBOSMIUM_VERSION}.tar.gz libosmium-${LIBOSMIUM_VERSION}.tar.gz

# Install OSMCoastline's dependencies
RUN apt autoremove -y && \
    add-apt-repository -y ppa:jonathonf/gcc && \
    apt update -y && \
    apt upgrade -y && \
    apt install -y gcc-7 g++-7 wget libutfcpp-dev libexpat1-dev zlib1g-dev libbz2-dev libboost-dev libsparsehash-dev libboost-program-options-dev libgeos++-dev doxygen graphviz pandoc spatialite-bin libspatialite-dev && \
    apt remove -y --purge gcc-5 && \
    apt autoremove -y && \
    update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-7 7 && \
    update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-7 7 && \
    update-alternatives --install /usr/bin/cpp cpp /usr/bin/cpp-7 7

RUN tar -zxf protozero-${PROTOZERO_VERSION}.tar.gz && \
    cd protozero-${PROTOZERO_VERSION} && \
    mkdir build && \
    cd build && \
    cmake .. && \
    make -j`nproc` && \
    make install

RUN tar -zxf libosmium-${LIBOSMIUM_VERSION}.tar.gz && \
    cd libosmium-${LIBOSMIUM_VERSION} && \
    mkdir build && \
    cd build && \
    cmake .. -DBUILD_EXAMPLES=OFF -DBUILD_TESTING=OFF -DCMAKE_BUILD_TYPE=Release -DINSTALL_GDALCPP=ON -DINSTALL_UTFCPP=ON && \
    make -j`nproc` && \
    make install

# Compile and install osmcoastline
RUN tar -zxf osmcoastline-${OSMCOASTLINE_VERSION}.tar.gz && \
    cd osmcoastline-${OSMCOASTLINE_VERSION} && \
    mkdir build && \
    cd build && \
    cmake .. && \
    make -j`nproc` && \
    make install

# Clean
RUN rm -Rf ./* && \
    apt remove -y --purge wget && \
    apt autoremove -y

WORKDIR /root
CMD osmcoastline --version
