#
# Credits: https://github.com/MilesChou/docker-phalcon
#
FROM php:7.4-alpine

LABEL maintainer="Ruud Boon <github.com/ruudboon>"

ARG PHALCON_VERSION=4.0.0
ARG PHALCON_EXT_PATH=php7/64bits

RUN set -xe && \
        # Download PSR, see https://github.com/jbboehr/php-psr
        curl -LO https://github.com/jbboehr/php-psr/archive/v${PSR_VERSION}.tar.gz && \
        tar xzf ${PWD}/v${PSR_VERSION}.tar.gz && \
        # Download Phalcon
        curl -LO https://github.com/phalcon/cphalcon/archive/v${PHALCON_VERSION}.tar.gz && \
        tar xzf ${PWD}/v${PHALCON_VERSION}.tar.gz && \
        docker-php-ext-install -j $(getconf _NPROCESSORS_ONLN) \
            ${PWD}/php-psr-${PSR_VERSION} \
            ${PWD}/cphalcon-${PHALCON_VERSION}/build/${PHALCON_EXT_PATH} \
        && \
        # Remove all temp files
        rm -r \
            ${PWD}/v${PSR_VERSION}.tar.gz \
            ${PWD}/php-psr-${PSR_VERSION} \
            ${PWD}/v${PHALCON_VERSION}.tar.gz \
            ${PWD}/cphalcon-${PHALCON_VERSION} \
        && \
        php -m

RUN apk --no-cache update && apk --no-cache add composer
RUN composer global require rector/rector
WORKDIR /project
ENTRYPOINT ["/root/.composer/vendor/bin/rector"]
CMD ["process", "--set",  "php74", "--dry-run"]
