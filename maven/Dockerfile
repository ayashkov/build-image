ARG source
FROM ${source}

ARG java_version
ARG maven_version

USER root
RUN apk update && \
    apk add --no-cache openjdk17-jre=~${java_version} \
        openjdk17-jdk=~${java_version} maven=~${maven_version}

USER build
WORKDIR /home/build
CMD [ "mvn" ]
