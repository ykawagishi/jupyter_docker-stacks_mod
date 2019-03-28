# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.
ARG BASE_CONTAINER=ykawagishi/test01
FROM $BASE_CONTAINER

LABEL maintainer=y.kawagishi@bitgroove.jp

USER root

# Install all OS dependencies for fully functional notebook server
RUN apt-get update && apt-get install -yq --no-install-recommends \
    build-essential \
    vim \
    git \
    netcat \
    pandoc \
    python-dev \
    tzdata \
    unzip \
    nano \
    curl \
    && rm -rf /var/lib/apt/lists/*

# Switch back to jovyan to avoid accidental container runs as root
# USER $NB_UID
