ARG source
FROM maven:${source}

RUN apk update \
    && apk add --no-cache --update chromium chromium-chromedriver \
    && apk del chromium chromium-chromedriver
