ARG ALPINE_URL

FROM alpine:latest AS downloader
ARG ALPINE_URL

RUN wget -O /rootfs.tar.gz "$ALPINE_URL"

FROM scratch

COPY --from=downloader /rootfs.tar.gz /
ADD /rootfs.tar.gz /

CMD ["/bin/sh"]