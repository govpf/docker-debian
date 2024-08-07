FROM debian:bullseye
MAINTAINER Léonard TAVAE <leonard.tavae@informatique.gov.pf>

ENV DEBIAN_FRONTEND noninteractive
ENV TZ Pacific/Tahiti

COPY bullseye/files/environment /etc/environment
COPY bullseye/files/locale.gen /etc/locale.gen

RUN echo "$TZ" > /etc/timezone \
    && rm -f /etc/localtime \
    && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
    && dpkg-reconfigure -f noninteractive tzdata \
    && apt-get update && apt-get install -y -o DPkg::Options::="--force-confnew" --no-install-recommends \
        git locales net-tools curl ca-certificates gnupg dirmngr \
    && curl https://bin.gov.pf/artifactory/ca/casit-prod2.crt > /usr/local/share/ca-certificates/casit-prod2.crt \
    && curl https://bin.gov.pf/artifactory/ca/cadsi-prod.crt > /usr/local/share/ca-certificates/cadsi-prod.crt \
    && update-ca-certificates \
    && locale-gen fr_FR.UTF-8 \
    && dpkg-reconfigure locales \
    && rm -rf /var/lib/apt/lists/*

ENV LANG fr_FR:UTF-8
ENV LANGUAGE fr
ENV LC_CTYPE fr_FR.utf8
ENV LC_MESSAGES fr_FR.utf8
ENV LC_ALL fr_FR.utf8
