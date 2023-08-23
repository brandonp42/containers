FROM docker.io/ubuntu AS build

COPY catatonit.sha256sum .

RUN export DEBIAN_FRONTEND=noninteractive \
    && apt-get update \
    && apt-get install -y wget \
    && wget -nv https://github.com/openSUSE/catatonit/releases/download/v0.1.7/catatonit.x86_64 \
    && sha256sum -c --ignore-missing --status catatonit.sha256sum \
    && install -m 00755 catatonit.x86_64 /usr/local/bin/catatonit

# ######################################################################
FROM docker.io/ubuntu
COPY --from=build /usr/local/bin/catatonit /usr/local/bin/catatonit
ENTRYPOINT [ "/usr/local/bin/catatonit", "--" ]
CMD [ "/bin/bash" ]

