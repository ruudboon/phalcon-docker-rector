#
# Credits: https://github.com/MilesChou/docker-phalcon
#
FROM php:7.3-alpine

LABEL maintainer="Ruud Boon <github.com/ruudboon>"

ARG PSR_VERSION=0.7.0
ARG PHALCON_VERSION=4.0.0
ARG PHALCON_EXT_PATH=php7/64bits

RUN set -xe && \
        # Download Phalcon
        curl -LO https://github.com/phalcon/cphalcon/archive/v${PHALCON_VERSION}.tar.gz && \
        tar xzf ${PWD}/v${PHALCON_VERSION}.tar.gz && \
        docker-php-ext-install -j $(getconf _NPROCESSORS_ONLN) \
            ${PWD}/cphalcon-${PHALCON_VERSION}/build/${PHALCON_EXT_PATH} \
        && \
        # Remove all temp files
        rm -r \
            ${PWD}/v${PHALCON_VERSION}.tar.gz \
            ${PWD}/cphalcon-${PHALCON_VERSION} \
        && \
        php -m

RUN apk --no-cache update && \
    apk --no-cache add composer && \
    composer global require rector/rector

WORKDIR /project
ENTRYPOINT ["/root/.composer/vendor/bin/rector"]
CMD ["process", "--set",  "phalcon40", "--dry-run"]
