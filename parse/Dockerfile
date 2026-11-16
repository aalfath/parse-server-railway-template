# Parse Server, built for the "Parse Server" Railway template.
# Official image, pinned by version and digest. To update: bump both, test, add a CHANGELOG entry.
FROM parseplatform/parse-server:9.11.0@sha256:c00740531b844228958080f37c6992f42dd37f49e312e5073c497f67ca61eb00

# Fixed defaults. Railway variables with the same names override them.
ENV PORT=1337 \
    PARSE_SERVER_HOST=:: \
    PARSE_SERVER_MOUNT_PATH=/parse \
    PARSE_SERVER_ALLOW_CLIENT_CLASS_CREATION=false

EXPOSE 1337
# Configuration comes from PARSE_SERVER_* environment variables (see README.md).
ENTRYPOINT ["node", "./bin/parse-server"]
