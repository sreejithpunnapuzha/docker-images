ARG ALPINE_URL

FROM alpine:latest AS downloader
ARG ALPINE_URL

RUN wget -O /rootfs.tar.gz "$ALPINE_URL"

FROM scratch

# copy into root
COPY --from=downloader /rootfs.tar.gz /rootfs.tar.gz

# now extract it
ADD rootfs.tar.gz /

CMD ["/bin/sh"]