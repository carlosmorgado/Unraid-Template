# Diaper Counter Unraid Template

This template lives in:

```text
carlosmorgado/diaper-counter/
```

inside `carlosmorgado/Unraid-Template`.

See the Diaper Counter app repo docs for the full deployment guides:

- [Unraid deployment](https://github.com/carlosmorgado/diaper-counter/blob/main/Unraid.md)
- [Cloudflare security](https://github.com/carlosmorgado/diaper-counter/blob/main/Cloudflare.md)

## Template

- `app.xml`: Diaper Counter web app image from GitHub Container Registry.

MongoDB and `Unraid-Cloudflared-Tunnel` should be installed from Unraid Community Apps instead of this template repo.

## Install Order

1. Create a private Docker network named `diaper-counter`.
2. Log in to `ghcr.io` from Unraid with a GitHub token that has `read:packages`.
3. Install MongoDB from Unraid Community Apps; set its container name to `diaper-counter-mongodb`, place it on the `diaper-counter` network, and set a strong root password.
4. Install `diaper-counter`; set the MongoDB connection string with the same password.
5. Install `Unraid-Cloudflared-Tunnel` from Unraid Community Apps; change its network from the default `bridge` to `diaper-counter` and set `TUNNEL_TOKEN`.
6. In Cloudflare Zero Trust, route your public hostname to `http://diaper-counter:8080`.

Keep the recommended container names, or update the app connection string and Cloudflare public-hostname service target to match your renamed containers. MongoDB should not expose a public host port.

If you publish this template under a different repository path, update the `TemplateURL` value in `app.xml`.
