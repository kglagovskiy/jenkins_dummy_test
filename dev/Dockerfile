FROM alpine
RUN apk upgrade && apk add cmake g++ make
RUN wget http://freefr.dl.sourceforge.net/project/boost/boost/1.60.0/boost_1_60_0.tar.gz &&\
    mkdir -p /usr/src &&\
    tar -zxf boost_1_60_0.tar.gz -C /usr/src &&\
    ln -s /usr/src/boost_1_60_0 /usr/src/boost &&\
    rm boost_1_60_0.tar.gz && \
    cd /usr/src/boost &&\
    bjam -d 0 release &&\
    bjam -d 0 --includedir=/usr/include --libdir=/usr/lib install &&\
    ln -s /usr/bin/bjam /usr/local/bin/b2

ENV BOOST_ROOT /usr/src/boost
ENV BOOST_BUILD_PATH /usr/src/boost/tools/build