# Jellystat

**Jellystat** is a free and open source statistics app for Jellyfin and Emby. It tracks live sessions, watch history, users and libraries, and turns them into statistics and reports.

> [!NOTE]
> This is Jellystat 2, a ground-up rewrite. It is in active development, so expect changes before the first stable release.

## Features

- **Live sessions:** see what's playing right now, updated in real time over WebSockets.
- **Activity:** full watch history across every user and library.
- **Users and libraries:** per-user and per-library overviews and statistics.
- **Statistics:** charts and breakdowns of what's watched, when and by whom.
- **Reports:** build custom reports, export them, and send them to webhooks on a schedule.
- **Backups:** scheduled and on-demand backups of your Jellystat data.
- **Geolocation:** optional IP geolocation through MaxMind GeoLite.
- **Translations:** the UI is translatable. See [Translating](#translating).

## Quick start

Jellystat runs as a single Docker container next to a PostgreSQL database.

1. Download [`docker-compose.yml`](docker-compose.yml) and [`.env.example`](.env.example) into an empty folder.
2. Copy `.env.example` to `.env` and set at least `DB_PASSWORD` and `JWT_KEY`.
3. Start it:

   ```bash
   docker compose up -d
   ```

4. Open `http://<your-server>:3000` and follow the setup wizard to connect your Jellyfin or Emby server.

Every setting is listed in [Environment Variables](#environment-variables) below.

## Environment Variables

| Env | Default | Example | Description |
|---|---|---|---|
| DB_HOST `REQUIRED` | `null` | `jellystat-db` or `192.168.0.5` | Hostname/IP of the PostgreSQL server. The compose file sets this to `jellystat-db` |
| DB_PORT | `5432` | `5432` | Port PostgreSQL is running on |
| DB_NAME | `jellystat` | `jellystat` | Name of the PostgreSQL database |
| DB_USERNAME `REQUIRED` | `null` | `jellystat` | Username used to connect to the database |
| DB_PASSWORD `REQUIRED` | `null` | `my-db-password` | Password used to connect to the database |
| JWT_KEY | random | `openssl rand -base64 48` | Key used to sign sign-in tokens. Must be at least 32 characters. If it isn't set, a new random key is generated on every start and everyone has to sign in again after a restart |
| TZ | `Etc/UTC` | `Europe/Paris` | Server timezone (see the [tz database list](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones#List)) |
| UI_URI | `null` | `https://ui.example.com` | Origin allowed to call the API from a browser (CORS). Only needed if you host the UI separately from the API |
| ALLOW_UNAUTHENTICATED_PASSWORD_RESET | `false` | `true` | Recovery mode for a locked-out admin. While it's on, **anyone who can reach Jellystat can reset local user passwords**. Turn it on, recover access, then turn it off and restart |
| MINIMUM_SECONDS_TO_INCLUDE_PLAYBACK | `1` | `10` | The minimum time (in seconds) to include a playback record, which can be used to exclude short playbacks |
| NEW_WATCH_EVENT_THRESHOLD_HOURS | `1` | `1-12` | The max time between watch sessions before a new session is created. A watch of the same item within this many hours is added onto the last session; after it, a new watch event is recorded |
| COMPLETION_THRESHOLD_PERCENTAGE | `90` | `95` | Percentage of an item that must be played for it to count as completed |
| JS_GEOLITE_ACCOUNT_ID | `null` | `123456` | [maxmind.com](https://www.maxmind.com/en/accounts/current/edit) account ID used for geolocating IP addresses |
| JS_GEOLITE_LICENSE_KEY | `null` | `ASDWdaSdawe2sd186` | License key you generate on MaxMind to use their geolocation service |
| REPORTS_MAX_ROWS | `10000` | `50000` | Maximum number of rows a single report can return |

The container listens on port `8080`. Mount a volume at `/app/backups` so backup files survive container updates.

## Getting help

- **Bugs and feature requests:** [open an issue](https://github.com/JellyStat/Jellystat/issues/new/choose) here. Please report all problems in this repo, even if you think they're in the UI or API. We'll move them if needed.
- **Questions and ideas:** use [Discussions](https://github.com/JellyStat/Jellystat/discussions).
- **Security issues:** don't open a public issue. See the [security policy](https://github.com/JellyStat/.github/blob/main/SECURITY.md).

## Project structure

Jellystat 2 is split across a few repositories in the [JellyStat organisation](https://github.com/JellyStat):

| Repository | What it is |
|---|---|
| **[Jellystat](https://github.com/JellyStat/Jellystat)** (this repo) | Start here: install docs, Docker Compose, issues and discussions |
| [JellyStat-API-Core](https://github.com/JellyStat/JellyStat-API-Core) | The backend: .NET API, database and background tasks. Its Docker image also serves the UI |
| [Jellystat-UI](https://github.com/JellyStat/Jellystat-UI) | The web interface: Next.js and Tailwind CSS |

## Contributing

Code contributions go to the repository for the part you're changing. Read the [contributing guide](https://github.com/JellyStat/.github/blob/main/CONTRIBUTING.md) first.

### Translating

Translations live in the UI repo. See [TRANSLATING.md](https://github.com/JellyStat/Jellystat-UI/blob/main/TRANSLATING.md) to add or improve a language.

## Licence

Jellystat is licensed under the [GNU General Public License v3.0](LICENSE).
