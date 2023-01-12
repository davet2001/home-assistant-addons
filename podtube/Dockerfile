# https://developers.home-assistant.io/docs/add-ons/configuration#add-on-dockerfile
ARG BUILD_FROM
FROM $BUILD_FROM

# Execute during the build of the image
ARG TEMPIO_VERSION BUILD_ARCH
RUN \
    curl -sSLf -o /usr/bin/tempio \
    "https://github.com/home-assistant/tempio/releases/download/${TEMPIO_VERSION}/tempio_${BUILD_ARCH}"
RUN \
    apk add --no-cache python3 py3-pip python3-dev \
    py3-psutil \
    py3-tornado \
    build-base \
    libffi-dev \
    libxslt-dev \
    libxml2-dev
RUN \
    pip install \
    wheel==0.38.4
RUN \
    pip install \
    misaka==2.1.1 \
    pytube==12.1.2  \
    feedgen==0.9.0 \
    requests==2.28.1

# Install pinned version of PodTube as it isn't on pypi and doesn't have tagged releases
ADD https://raw.githubusercontent.com/aquacash5/PodTube/0052a3aabeea83ba6e7c4da3b02a52d6aa7c6244/podtube.py /usr/bin/

# Copy root filesystem
COPY rootfs /

