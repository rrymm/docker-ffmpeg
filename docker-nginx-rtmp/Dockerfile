From dorftv/ffmpeg-core

ENV DEBIAN_FRONTEND noninteractive
ENV PATH $PATH:/usr/local/nginx/sbin
ENV NGINX_VERSION=1.13.5



RUN apt-get update && apt-get install -y libpcre3-dev zlib1g-dev libssl-dev unzip libxslt1-dev git && \
    mkdir /src && mkdir /config && mkdir /logs && mkdir /data && mkdir /static && cd /src && \
    wget http://nginx.org/download/nginx-$NGINX_VERSION.tar.gz && tar -xzvf nginx-$NGINX_VERSION.tar.gz && \
    git clone https://github.com/sergey-dryabzhinsky/nginx-rtmp-module.git &&  cd /src/nginx-$NGINX_VERSION && \
    ./configure \
                        --with-http_addition_module \
                        --with-http_gunzip_module \
                        --with-http_gzip_static_module \
                        --with-http_sub_module \
                        --with-stream \
                        --with-stream_ssl_module \
                        --with-mail \
                        --with-mail_ssl_module \
                        --with-threads \
                        --with-pcre-jit \
                        --with-http_ssl_module \
			--with-http_xslt_module \
			--with-http_v2_module \
			--with-ipv6 \
                        --add-module=/src/nginx-rtmp-module --conf-path=/config/nginx.conf --error-log-path=/logs/error.log --http-log-path=/logs/access.log && \
    make -j5 && make install && rm -rf /src && apt-get clean && apt-get autoremove

ADD static /static
ADD nginx.conf /config/nginx.conf

CMD "nginx"


