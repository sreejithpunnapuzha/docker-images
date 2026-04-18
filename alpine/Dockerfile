ARG ALPINE_URL

FROM alpine:latest AS downloader
ARG ALPINE_URL

RUN wget -O /rootfs.tar.gz "$ALPINE_URL" \
    && mkdir /rootfs \
    && tar -xzf /rootfs.tar.gz -C /rootfs

FROM scratch

COPY --from=downloader /rootfs/ /

CMD ["/bin/sh"]