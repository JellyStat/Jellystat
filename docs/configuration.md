# Configuration

Jellystat is configured with environment variables. With the provided [`docker-compose.yml`](../docker-compose.yml), put them in your `.env` file.

## Database

| Variable | Required | Default | Description |
|---|---|---|---|
| `DB_HOST` | Yes | | Hostname or IP of the PostgreSQL server. The compose file sets this to `jellystat-db`. |
| `DB_PORT` | | `5432` | PostgreSQL port. |
| `DB_NAME` | | `jellystat` | Database name. |
| `DB_USERNAME` | Yes | | Database user. |
| `DB_PASSWORD` | Yes | | Database password. |

## Security

| Variable | Required | Default | Description |
|---|---|---|---|
| `JWT_KEY` | Recommended | random per start | Key used to sign sign-in tokens. Must be at least 32 characters. If it isn't set, Jellystat generates a new key on every start and everyone has to sign in again after a restart. |
| `UI_URI` | | | Origin allowed to call the API from a browser (CORS), for example `https://ui.example.com`. Only needed if you host the UI separately from the API. |
| `ALLOW_UNAUTHENTICATED_PASSWORD_RESET` | | `false` | Recovery mode for a locked-out admin. While it's on, **anyone who can reach Jellystat can reset local user passwords**. Turn it on, recover access, then turn it off and restart. |

## Playback tracking

| Variable | Default | Description |
|---|---|---|
| `MINIMUM_SECONDS_TO_INCLUDE_PLAYBACK` | `1` | Playbacks shorter than this many seconds aren't recorded. |
| `NEW_WATCH_EVENT_THRESHOLD_HOURS` | `1` | If the same item is played again within this many hours, it's added to the previous watch instead of creating a new one. |
| `COMPLETION_THRESHOLD_PERCENTAGE` | `90` | Percentage of an item that must be played for it to count as completed. |

## Geolocation

Jellystat can look up the location of client IP addresses with MaxMind GeoLite. Create a free account at [maxmind.com](https://www.maxmind.com) to get these values.

| Variable | Description |
|---|---|
| `JS_GEOLITE_ACCOUNT_ID` | MaxMind account ID. |
| `JS_GEOLITE_LICENSE_KEY` | MaxMind licence key. |

## Reports

| Variable | Default | Description |
|---|---|---|
| `REPORTS_MAX_ROWS` | `10000` | Maximum number of rows a single report can return. |

## General

| Variable | Default | Description |
|---|---|---|
| `TZ` | `Etc/UTC` | Server timezone, as a [tz database name](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) such as `Europe/Paris`. |

## Storage

| Container path | Contents |
|---|---|
| `/app/backups` | Backup files. Mount a volume here so backups survive container updates. |

The container listens on port `8080`.
