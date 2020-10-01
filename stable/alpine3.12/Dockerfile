FROM alpine:3.12
ENV LANG C.UTF-8

RUN set -eux ;\
        apk add --no-cache \
                bash \
		ca-certificates \
                gcc \
		openssl-dev \
                zlib-dev \
                make \
                tar \
                wget \
        ;

# install stable
# see https://github.com/Shopify/truffleruby-shopify/blob/master/doc/user/standalone-distribution.md
ENV TRUFFLERUBY_VERSION 20.2.0

RUN set -eux ;\
        wget -q https://github.com/oracle/truffleruby/releases/download/vm-$TRUFFLERUBY_VERSION/truffleruby-$TRUFFLERUBY_VERSION-linux-amd64.tar.gz ;\
        tar -xzf truffleruby-$TRUFFLERUBY_VERSION-linux-amd64.tar.gz -C /usr/local --strip-components=1 ;\
        rm truffleruby-$TRUFFLERUBY_VERSION-linux-amd64.tar.gz ;\
        /usr/local/lib/truffle/post_install_hook.sh ;\
        ruby --version ;\
        gem --version ;\
        bundle --version 

# don't create ".bundle" in all our apps
ENV GEM_HOME /usr/local/bundle
ENV BUNDLE_SILENCE_ROOT_WARNING=1 \
        BUNDLE_APP_CONFIG="$GEM_HOME"
ENV PATH $GEM_HOME/bin:$PATH
# adjust permissions of a few directories for running "gem install" as an arbitrary user
RUN mkdir -p "$GEM_HOME" && chmod 777 "$GEM_HOME"

CMD [ "irb" ]
