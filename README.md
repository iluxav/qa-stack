# qa-stack

A classic **web + server + db** stack, spanning three GitHub repos, expressed
as one ply composition. Point a single deployment order at this repo and the
host builds and wires the whole thing — no CI, no registry, no Docker.

## Deploy

On a host prepared with `sudo ply setup --edge`:

```sh
sudo tee /var/lib/ply/deployments/qa.toml <<'ORDER'
repo = "https://github.com/iluxav/qa-stack"
ORDER
```

Within a minute: `db` (postgres@17), `server`
([qa-server](https://github.com/iluxav/qa-server), built on host) and `web`
([qa-web](https://github.com/iluxav/qa-web), built on host) are running and
wired. Visit `http://<host>:8080`.

## What it demonstrates

- a multi-repo product as **one reviewable recipe**
- **build-on-host** from source — no registry hop
- `after` **auto-wires** service addresses (no hardcoded hosts)
- per-repo redeploy: push to qa-web, only web rebuilds
