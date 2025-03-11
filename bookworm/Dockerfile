FROM debian:bookworm
MAINTAINER Léonard TAVAE <leonard.tavae@informatique.gov.pf>

ENV DEBIAN_FRONTEND noninteractive
ENV TZ Pacific/Tahiti

COPY bookworm/files/environment /etc/environment
COPY bookworm/files/locale.gen /etc/locale.gen

RUN echo "$TZ" > /etc/timezone \
    && rm -f /etc/localtime \
    && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
    && dpkg-reconfigure -f noninteractive tzdata \
    && apt-get update && apt-get install -y -o DPkg::Options::="--force-confnew" --no-install-recommends \
        git locales net-tools curl ca-certificates gnupg dirmngr \
    && locale-gen fr_FR.UTF-8 \
    && dpkg-reconfigure locales \
    && rm -rf /var/lib/apt/lists/*

COPY install_certs /tmp/install_certs
RUN  bash -xe /tmp/install_certs

ENV LANG fr_FR:UTF-8
ENV LANGUAGE fr
ENV LC_CTYPE fr_FR.utf8
ENV LC_MESSAGES fr_FR.utf8
ENV LC_ALL fr_FR.utf8
