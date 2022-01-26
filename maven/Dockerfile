ARG source
FROM ${source}

ARG maven_version

RUN apk update && \
    apk add --no-cache openjdk17-jre openjdk17-jdk maven=~${maven_version}

USER build
WORKDIR /home/build
CMD [ "mvn" ]
