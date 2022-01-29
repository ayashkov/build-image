ARG source
FROM ${source}

ARG angular_version=latest

USER root
RUN apk update && \
    apk add --no-cache alpine-sdk python3 && \
    npm install -g @angular/cli@${angular_version} && \
    apk del alpine-sdk python3 && \
    npm cache clean --force

USER build
WORKDIR /home/build
CMD [ "ng" ]
