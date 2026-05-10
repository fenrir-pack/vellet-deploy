# vellet-deploy

Public deploy manifest for [Vellet](https://github.com/fenrir-pack/vellet-app).

This repo exists only so platforms like **Hostinger Docker Manager** — which
clone the source repo of the compose URL before deploying — can fetch a
manifest without needing credentials against the private application repo.

## Usage

Point Hostinger Docker Manager (or any compose-by-URL runner) at:

```
https://raw.githubusercontent.com/fenrir-pack/vellet-deploy/main/docker-compose.prod.yml
```

The compose references private images on GHCR:

- `ghcr.io/fenrir-pack/vellet-api`
- `ghcr.io/fenrir-pack/vellet-caddy`

The VPS docker daemon must be authenticated against GHCR once:

```sh
echo "<PAT_with_read:packages>" | docker login ghcr.io -u <github-user> --password-stdin
```

All secrets (`POSTGRES_PASSWORD`, `JWT_SECRET`, `CORS_ORIGINS`, OAuth IDs, …)
are supplied at deploy time through the Hostinger env editor or a `.env` file
on the VPS — never committed here.

## Updating

This file is kept in sync with the canonical version that lives in
[`fenrir-pack/vellet-app`](https://github.com/fenrir-pack/vellet-app/blob/main/docker-compose.prod.yml).
Any change should originate there and be propagated here.
