ARG source
FROM maven:${source}

RUN apk update \
    && apk add --no-cache alsa-lib at-spi2-atk at-spi2-core atk cairo \
        cups-libs dbus-libs eudev-libs expat ffmpeg-libs flac \
        fontconfig freetype glib harfbuzz lcms2 libatomic libdrm \
        libevent libgcc libjpeg-turbo libpng libstdc++ libwebp \
        libx11 libxcb libxcomposite libxdamage libxext libxfixes \
        libxkbcommon libxml2 libxrandr libxshmfence libxslt mesa-gbm \
        musl nspr nss opus pango re2 snappy ttf-opensans xdg-utils \
        zlib
