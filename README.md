# Parse Server on Railway

[![Deploy on Railway](https://railway.com/button.svg)](https://railway.com/new/template/parse-server-1?utm_medium=integration&utm_source=button&utm_campaign=parse-server)

This repo is the source of the [Parse Server](https://railway.com/deploy/parse-server-1) Railway template. It deploys:

| Service | Built from | Version |
|---|---|---|
| `parse` | [`parse/Dockerfile`](parse/Dockerfile) | Parse Server 9.11.0 (`parseplatform/parse-server`, pinned by digest) |
| `dashboard` | [`dashboard/Dockerfile`](dashboard/Dockerfile) | Parse Dashboard 10.0.0 (`parseplatform/parse-dashboard`, pinned by digest) |
| `MongoDB` | `mongo:8.0.38` image (pinned by digest) | MongoDB 8.0, data on a volume at `/data/db` |

Parse Server serves the API at `https://YOUR-PARSE-DOMAIN/parse`, with a health check at `/parse/health`. Parse Dashboard is on its own domain, behind a login. Uploaded files go to MongoDB GridFS, so no other storage is needed.

## Variables

Every variable has a default, so the template deploys without questions.

**`parse`**
- `PARSE_SERVER_APPLICATION_ID`, `PARSE_SERVER_MASTER_KEY`: generated secrets. Your client apps need the application ID. Keep the master key private.
- `PARSE_SERVER_DATABASE_URI`: the MongoDB service's private URL, database `parse`.
- `PARSE_PUBLIC_SERVER_URL`, `PARSE_SERVER_URL`: the public URL and the URL Parse uses to call itself.
- `PARSE_SERVER_MASTER_KEY_IPS`: open to all IPs, because the dashboard sends the master key from your browser. Narrow it if you don't use the dashboard.
- `PARSE_SERVER_ALLOW_CLIENT_CLASS_CREATION`: `false`. Create classes in the dashboard or with the master key.
- `PORT`, `PARSE_SERVER_HOST`, `PARSE_SERVER_MOUNT_PATH`: `1337`, `::`, `/parse`.

**`dashboard`**
- `PARSE_DASHBOARD_USER_ID` (`admin`) and `PARSE_DASHBOARD_USER_PASSWORD` (generated): the dashboard login. Find the password in the service's Variables tab.
- `PARSE_DASHBOARD_SERVER_URL`, `PARSE_DASHBOARD_APP_ID`, `PARSE_DASHBOARD_MASTER_KEY`: references to the `parse` service.
- `PARSE_DASHBOARD_COOKIE_SESSION_SECRET`: generated secret.

**`MongoDB`**
- `MONGO_INITDB_ROOT_USERNAME` (`mongo`) and `MONGO_INITDB_ROOT_PASSWORD` (generated), plus `MONGO_URL` for other services.
- `GLIBC_TUNABLES=glibc.pthread.rseq=1`: keeps MongoDB 8 from crash-looping on hosts running Linux 6.19 or later.

Optional settings (email adapter for password resets, S3 file storage, Cloud Code, push) are normal `PARSE_SERVER_*` variables; see the [Parse Server options](https://parseplatform.org/parse-server/api/master/ParseServerOptions.html).

## Updates

Railway sends everyone who deployed the template an "update available" notice when a change is merged to `main` here. Each update bumps the pinned image and adds an entry to [CHANGELOG.md](CHANGELOG.md). Read it before you apply the update. Parse Server and MongoDB upgrades are one-way, so back up your database first.
