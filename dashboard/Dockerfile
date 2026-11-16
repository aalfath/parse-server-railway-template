# Parse Dashboard, built for the "Parse Server" Railway template.
# Official image, pinned by version and digest. To update: bump both, test, add a CHANGELOG entry.
FROM parseplatform/parse-dashboard:10.0.0@sha256:19cce9020708896682c820bbff6261001bb676226ec64d9865d3ead9584de93d

# Fixed defaults. Railway variables with the same names override them.
# TRUST_PROXY=1 lets the dashboard see Railway's HTTPS edge, so login works without allowInsecureHTTP.
ENV PORT=4040 \
    PARSE_DASHBOARD_TRUST_PROXY=1

EXPOSE 4040
# Configuration comes from PARSE_DASHBOARD_* environment variables (see README.md).
ENTRYPOINT ["node", "Parse-Dashboard/index.js"]
