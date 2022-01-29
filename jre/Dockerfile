ARG source
FROM ${source}

ARG jre_version

RUN apk update && \
    apk add --no-cache openjdk17-jre-headless=~${jre_version}

CMD [ "java" ]
