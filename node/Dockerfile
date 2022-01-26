ARG source
FROM ${source}

ARG node_version
ARG npm_version

RUN addgroup -g 1000 build && \
    adduser -u 1000 -G build -s /bin/sh -D build && \
    apk update && \
    apk add --no-cache nodejs=~${node_version} npm=~${npm_version}

USER build
WORKDIR /home/build
CMD [ "node" ]
