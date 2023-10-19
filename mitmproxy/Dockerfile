ARG BUILD_FROM
FROM $BUILD_FROM AS BUILD

# In future we may be able to install mitmproxy directly.
# (currently in alpine testing and arm versions are not in the repos)
# The two install commands work, but only on x86 (no use for Rpi).
#RUN echo "@testing https://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories
#apk add --no-cache mitmproxy@testing=10.1.1-r0 \

RUN \
    apk add --no-cache \
    python3=3.11.6-r0 \
    python3-dev=3.11.6-r0 \
    py3-pip=23.1.2-r0 \
    py3-wheel=0.40.0-r1 \
    py3-six=1.16.0-r6 \
    py3-parsing=3.0.9-r2 \
    py3-certifi=2023.7.22-r0 \
    py3-brotli=1.0.9-r14 \
    py3-pyperclip=1.8.2-r2 \
    py3-cryptography=41.0.3-r0 \
    py3-asgiref=3.6.0-r1 \
    py3-msgpack=1.0.5-r1 \
    py3-passlib=1.7.4-r4 \
    py3-protobuf=4.21.12-r1 \
    py3-openssl=23.2.0-r0 \
    py3-ruamel.yaml=0.17.28-r0 \
    py3-sortedcontainers=2.4.0-r3 \
    py3-tornado=6.3.2-r0 \
    py3-wsproto=1.2.0-r2 \
    py3-flask=2.2.5-r0 \
    py3-h11=0.14.0-r2 \
    py3-h2=4.1.0-r2 \
    py3-hyperframe=6.0.1-r2 \
    py3-kaitaistruct=0.10-r3 \
    py3-ldap3=2.9.1-r2 \
    rust=1.71.1-r0 \
    cargo=1.71.1-r0 \
    bsd-compat-headers=0.7.2-r5 \
    build-base=0.5-r3 \
    libffi=3.4.4-r2 \
    libffi-dev=3.4.4-r2 \
    libstdc++=12.2.1_git20220924-r10 \
    openssl=3.1.3-r0 \
    openssl-dev=3.1.3-r0 \
    patch=2.7.6-r10



RUN pip3 install --no-cache-dir --user --upgrade mitmproxy==10.1.1

# patch mitmproxy to allow running with relative paths not in the server root
# Now that https://github.com/mitmproxy/mitmproxy/pull/6411 is merged,
# mitmproxy >10.1.1 should not need the patch lines below.
COPY mitmweb_relpath.patch /mitmweb_relpath.patch
RUN patch -u /root/.local/lib/python3.11/site-packages/mitmproxy/tools/web/templates/index.html -i /mitmweb_relpath.patch
RUN sed -i 's/"\/updates\"/location\.pathname\+"updates"/' /root/.local/lib/python3.11/site-packages/mitmproxy/tools/web/static/app.js

FROM $BUILD_FROM AS RUNNING

RUN apk add --no-cache \
    python3=3.11.6-r0 \
    zstd=1.5.5-r4 \
    haproxy=2.6.15-r0 \
    ca-certificates=20230506-r0

RUN rm -rf /var/cache/apk/* /tmp/*

COPY --from=BUILD /root/.local /root/.local
COPY --from=BUILD /usr/lib/python3.11/site-packages /usr/lib/python3.11/site-packages

ENV PATH /root/.local/bin:$PATH

ENTRYPOINT [ "/init" ]
CMD []
COPY root /

