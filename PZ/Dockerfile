FROM cm2network/steamcmd:root as build_stage

LABEL maintainer="vzylexy@gmail.com"

ENV STEAMAPPID 380870
ENV STEAMAPP pzserver
ENV STEAMAPPDIR "${HOMEDIR}/${STEAMAPP}-dedicated"
ENV DLURL 

RUN set -x \
    && apt-get update \
    && apt-get install -y --no-install-recommends --no-install-suggests \
    wget=1.21-1+deb11u1 \
    ca-certificates=20210119 \
    lib32z1=1:1.2.11.dfsg-2+deb11u2 \
    tini=0.19.0-1 \
    libc6-dev=2.31-13+deb11u7 \
    file=1:5.39-3+deb11u1 \
    && mkdir -p "${STEAMAPPDIR}" \
    && wget --max-redirect=30 "${DLURL}/master/scripts/run.sh" -O "${HOMEDIR}/run.sh" \
    && chmod +x "${HOMEDIR}/run.sh" \
    && chown -R "${USER}:${USER}" "${HOMEDIR}/run.sh" "${STEAMAPPDIR}" \
    # Clean up
    && rm -rf /var/lib/apt/lists/*

FROM build_stage AS bullseye-base

ENV SERVER_PORT=16261 \
    SERVER_NAME="New \ "${STEAMAPP}" Server" \
    SERVER_LOG_PATH="logs_output/outputlog_server.txt"
    
USER ${USER}

WORKDIR ${HOMEDIR}

STOPSIGNAL SIGINT

ENTRYPOINT [  ]

EXPOSE 16261/udp \
    16262/udp