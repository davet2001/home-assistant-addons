ARG BUILD_FROM
FROM $BUILD_FROM AS BUILD

RUN echo "@testing https://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories

RUN \
    apk add --no-cache \
    mitmproxy@testing=10.1.1-r0 \
    haproxy=2.6.15-r0 \
    patch=2.7.6-r10

COPY mitmweb_relpath.patch /mitmweb_relpath.patch
RUN patch -u /usr/lib/python3.11/site-packages/mitmproxy/tools/web/templates/index.html -i /mitmweb_relpath.patch
RUN sed -i 's/"\/updates\"/location\.pathname\+"updates"/' /usr/lib/python3.11/site-packages/mitmproxy/tools/web/static/app.js

ENV PATH /root/.local/bin:$PATH

ENTRYPOINT [ "/init" ]
CMD []
COPY root /

