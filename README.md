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

Every setting is listed in [docs/configuration.md](docs/configuration.md).

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
