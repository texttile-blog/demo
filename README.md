# deploy-demo

Hosts the texttile demo instance on Fly.io from the published image
`ghcr.io/texttile-blog/texttile:latest`: app `texttile-demo` on
demo.texttile.blog. The application code lives at
[texttile-blog/texttile](https://github.com/texttile-blog/texttile), and
that repository deploys its own source to a different app,
`texttile-staging` on staging.texttile.blog. The demo never builds from
source; it runs what was published.

## How it deploys

- A push to `main` in this repo deploys.
- A daily cron (06:00 UTC) redeploys, which pulls the latest image.
- Run the workflow by hand for an immediate update: `gh workflow run deploy`.

The app migrates its database at boot. An update is only: pull image, restart.
All state lives on the Fly volume (`/data`).

## New instance

1. Copy this repo.
2. Run the one-time setup commands from the header of `fly.toml`.
3. Change `app` and `PHX_HOST` in `fly.toml`.
4. Create a deploy token (`fly tokens create deploy -a <name>`) and store it as
   the `FLY_API_TOKEN` secret of the new repo.
