ARG source
FROM ${source}

ARG node_version

RUN apk update && \
    apk add --no-cache nodejs=~${node_version}

CMD [ "node" ]
