FROM node:10-alpine

LABEL MAINTAINER Yamashita <darum@yamas.xyz>

RUN apk --no-cache update && \
    apk --no-cache upgrade && \
    apk --no-cache add \
        lcms2-dev \
        libpng-dev \
		g++ \
		make \
		zlib-dev \
        openssl \
        automake \
		autoconf \
        bash && \
    npm update -g npm && \
    npm cache verify

ENV HOME=/laravel
WORKDIR /laravel

ENTRYPOINT ["npm"]
CMD ["-h"]

