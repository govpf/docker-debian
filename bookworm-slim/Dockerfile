# Use the official Debian 12 slim image as a base.
FROM debian:bookworm-slim

# Use standardized labels for authorship and metadata.
LABEL org.opencontainers.image.authors="Tanguy Jouannic <tanguy.jouannic@administration.gov.pf>"

# Set environment variables.
ENV DEBIAN_FRONTEND="noninteractive"
ENV TZ="Pacific/Tahiti"
ENV LANG="fr_FR.UTF-8"
ENV LANGUAGE="fr"
ENV LC_ALL="fr_FR.UTF-8"

# Copy configuration files.
COPY bookworm-slim/files/environment /etc/environment
COPY bookworm-slim/files/locale.gen /etc/locale.gen

# Consolidate package installation, timezone, and locale setup into a single RUN instruction.
# This reduces the number of image layers.
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        ca-certificates \
        curl \
        dirmngr \
        git \
        gnupg \
        locales \
        net-tools && \
    # Configure timezone.
    ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo "$TZ" > /etc/timezone && \
    # Configure locales.
    locale-gen fr_FR.UTF-8 && \
    # Clean up apt cache to reduce image size.
    rm -rf /var/lib/apt/lists/*

# Copy and execute the certificate installation script in a single layer.
# This ensures temporary files are removed and not left in the final image.
COPY install_certs /tmp/install_certs
RUN bash -xe /tmp/install_certs && rm -f /tmp/install_certs