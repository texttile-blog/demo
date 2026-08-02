# texttile-deploy

Hosts one texttile instance on Fly.io from the published image
`ghcr.io/texttile-blog/texttile:latest`. The application code lives at
[texttile-blog/texttile](https://github.com/texttile-blog/texttile).

## How it deploys

- A push to `main` in this repo deploys.
- A weekly cron (Monday 06:00 UTC) redeploys, which pulls the latest image.
- Run the workflow by hand for an immediate update: `gh workflow run deploy`.

The app migrates its database at boot. An update is only: pull image, restart.
All state lives on the Fly volume (`/data`).

## New instance

1. Copy this repo.
2. Run the one-time setup commands from the header of `fly.toml`.
3. Change `app` and `PHX_HOST` in `fly.toml`.
4. Create a deploy token (`fly tokens create deploy -a <name>`) and store it as
   the `FLY_API_TOKEN` secret of the new repo.
