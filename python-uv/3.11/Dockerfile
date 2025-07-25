FROM        --platform=$TARGETOS/$TARGETARCH ghcr.io/astral-sh/uv:python3.11-bookworm-slim

LABEL       author="Ethan Coward" maintainer="contact@ethancoward.dev"

RUN         apt update \
            && apt -y install git gcc g++ ca-certificates dnsutils curl iproute2 ffmpeg procps tini \
            && useradd -m -d /home/container container

# Set UV environment variables for better Docker integration
ENV         UV_SYSTEM_PYTHON=1
ENV         UV_TOOL_BIN_DIR=/usr/local/bin

USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

STOPSIGNAL SIGINT

COPY        --chown=container:container ./../entrypoint.sh /entrypoint.sh
RUN         chmod +x /entrypoint.sh
ENTRYPOINT    ["/usr/bin/tini", "-g", "--"]
CMD         ["/entrypoint.sh"]