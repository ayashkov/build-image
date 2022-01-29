ARG source
FROM ${source}

ARG npm_version

RUN addgroup -g 1000 build && \
    adduser -u 1000 -G build -s /bin/sh -D build && \
    apk update && \
    apk add --no-cache npm=~${npm_version} chromium chromium-chromedriver

ENV CHROME_BIN=/usr/bin/chromium-browser

USER build
WORKDIR /home/build
CMD [ "npm" ]
