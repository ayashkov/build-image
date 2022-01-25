ARG java_version
ARG maven_version
FROM maven:${maven_version}-eclipse-temurin-${java_version}-alpine

RUN apk update \
    && apk add --no-cache --update chromium chromium-chromedriver \
    && apk del chromium chromium-chromedriver
