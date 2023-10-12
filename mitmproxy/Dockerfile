ARG BUILD_FROM
FROM $BUILD_FROM AS BUILD

RUN echo "@testing https://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories

RUN \
    apk add --no-cache \
    mitmproxy@testing=10.1.1-r0 \
    haproxy=2.6.15-r0

# COPY --from=BUILD /root/.local /root/.local
# COPY --from=BUILD /usr/lib/python3.9/site-packages /usr/lib/python3.8/site-packages

ENV PATH /root/.local/bin:$PATH

ENTRYPOINT [ "/init" ]
CMD []
COPY root /

