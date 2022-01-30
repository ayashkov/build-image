ARG source
FROM ${source}

ARG maven_version

USER root
RUN apk update && \
    apk add --no-cache openjdk17-jre-headless
RUN apk add --no-cache apkopenjdk17-jre
RUN apk add --no-cache openjdk17-jdk
RUN apk add --no-cache maven=~${maven_version}

USER build
WORKDIR /home/build
CMD [ "mvn" ]
