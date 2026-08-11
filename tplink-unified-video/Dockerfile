ARG BUILD_FROM
FROM ${BUILD_FROM}

ARG BUILD_ARCH
ARG GO2RTC_VERSION=v1.9.14

RUN apk add --no-cache ca-certificates curl jq openssl     && case "$BUILD_ARCH" in         amd64) GO2RTC_ARCH="amd64" ;;         aarch64) GO2RTC_ARCH="arm64" ;;         armv7) GO2RTC_ARCH="arm" ;;         armhf) GO2RTC_ARCH="armv6" ;;         i386) GO2RTC_ARCH="i386" ;;         *) echo "Unsupported arch: $BUILD_ARCH" >&2; exit 1 ;;     esac     && curl -fsSL -o /usr/local/bin/go2rtc         "https://github.com/AlexxIT/go2rtc/releases/download/${GO2RTC_VERSION}/go2rtc_linux_${GO2RTC_ARCH}"     && chmod +x /usr/local/bin/go2rtc

COPY rootfs /
RUN chmod +x /etc/services.d/tplink-unified-video/run
