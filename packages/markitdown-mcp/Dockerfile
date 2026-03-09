FROM python:3.13-slim-bullseye

ENV DEBIAN_FRONTEND=noninteractive
ENV EXIFTOOL_PATH=/usr/bin/exiftool
ENV FFMPEG_PATH=/usr/bin/ffmpeg
ENV MARKITDOWN_ENABLE_PLUGINS=True

# Runtime dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    ffmpeg \
    exiftool

# Cleanup
RUN rm -rf /var/lib/apt/lists/*

WORKDIR /app

# Copy packages from repository root context
COPY packages/markitdown /app/packages/markitdown
COPY packages/markitdown-mcp /app/packages/markitdown-mcp

# Install both packages
RUN pip --no-cache-dir install \
    /app/packages/markitdown[all] \
    /app/packages/markitdown-mcp

WORKDIR /workdir

# Default USERID and GROUPID
ARG USERID=nobody
ARG GROUPID=nogroup

USER $USERID:$GROUPID

ENTRYPOINT [ "markitdown-mcp" ]
