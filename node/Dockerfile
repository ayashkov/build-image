ARG source
FROM ${source}

ARG node_version
ARG npm_version

RUN apk update && \
    apk add --no-cache nodejs=~${node_version} npm=~${npm_version}

CMD [ "node" ]
