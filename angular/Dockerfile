ARG source
FROM ${source}

ARG angular_version=latest

USER root
RUN apk update && \
    apk add --no-cache alpine-sdk python3 chromium chromium-chromedriver && \
    npm install -g @angular/cli@${angular_version} && \
    apk del alpine-sdk python3 && \
    npm cache clean --force

ENV CHROME_BIN=/usr/bin/chromium-browser

USER build
WORKDIR /home/build
CMD [ "ng" ]
