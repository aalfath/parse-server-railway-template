# Changelog

Changes to the [Parse Server Railway template](https://railway.com/deploy/parse-server-1). Breaking changes come first in each entry. A merge to `main` sends an "update available" notice to everyone who deployed the template from this repo: read the entry before you apply it.

## 2026-11-16: Parse Server 9.11.0, Parse Dashboard 10.0.0

**Breaking for people moving from the old image-based template (Parse Server 8.6, Dashboard 9.2):**
- Parse Server 9 sets `enableInsecureAuthAdapters` to `false` by default. If your app logs in through an auth adapter that Parse marks insecure, set `PARSE_SERVER_ENABLE_INSECURE_AUTH_ADAPTERS=true` on the `parse` service or move to a secure adapter. See the [Parse Server 9.0.0 release notes](https://github.com/parse-community/parse-server/releases/tag/9.0.0).
- Parse Dashboard 10 needs Node 22 or later. The official image already ships Node 24.

**Changes:**
- The `parse` and `dashboard` services now build from this repo (`parse/` and `dashboard/`), so deployers get update notices.
- `parse`: `parseplatform/parse-server:9.11.0@sha256:c00740531b844228958080f37c6992f42dd37f49e312e5073c497f67ca61eb00`.
- `dashboard`: `parseplatform/parse-dashboard:10.0.0@sha256:19cce9020708896682c820bbff6261001bb676226ec64d9865d3ead9584de93d`.
- MongoDB (template config, not this repo): `mongo:8.0.38`, pinned by digest, with `GLIBC_TUNABLES=glibc.pthread.rseq=1`. Without it, MongoDB 8 crash-loops on hosts running Linux 6.19 or later ([SERVER-121912](https://jira.mongodb.org/browse/SERVER-121912)).
