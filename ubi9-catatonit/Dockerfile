FROM registry.access.redhat.com/ubi9 AS build

COPY catatonit.sha256sum .

RUN dnf install -y wget \
    && wget -nv https://github.com/openSUSE/catatonit/releases/download/v0.1.7/catatonit.x86_64 \
    && sha256sum -c --ignore-missing --status catatonit.sha256sum \
    && install -m 00755 catatonit.x86_64 /usr/local/bin/catatonit

# ######################################################################
FROM registry.access.redhat.com/ubi9
COPY --from=build /usr/local/bin/catatonit /usr/local/bin/catatonit
ENTRYPOINT [ "/usr/local/bin/catatonit", "--" ]
CMD [ "/bin/bash" ]
