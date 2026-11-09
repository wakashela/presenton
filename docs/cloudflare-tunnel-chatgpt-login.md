# Docker, Cloudflare Tunnel, and ChatGPT Login

This guide records the setup used to access Presenton at `https://presenton.unde.co.tz/` through a Cloudflare Tunnel and connect a ChatGPT account.

## Start Presenton

In the repository root, add the public address to `.env` beside `docker-compose.yml`:

```dotenv
PRESENTON_PUBLIC_URL=https://presenton.unde.co.tz
```

This setting gives generated download, edit, and preview links the public origin. Start or recreate the production service:

```bash
docker compose up -d production
```

Compose maps host port `5001` to the application's port `80` by default. Point the Cloudflare Tunnel hostname at `http://localhost:5001` when the tunnel runs on the same host. Set `PRESENTON_HTTP_HOST_PORT` if a different host port is needed and update the tunnel target accordingly. Compose also maps port `1455` for the Codex OAuth callback.

Check the service and follow its logs:

```bash
docker compose ps
docker compose logs -f production
```

The production service persists application data in `./app_data`; protect this directory because it can contain credentials and other sensitive data.

## Connect ChatGPT

1. Open the public URL, go to Settings, and select the ChatGPT provider.
2. Start sign-in and authenticate with your ChatGPT account in the new browser tab.
3. If the browser cannot connect to `http://localhost:1455/auth/callback`, copy the complete URL from its address bar. `localhost` refers to the machine running the browser, so the callback may not reach a remote Presenton server.
4. Return to the original Presenton settings tab and paste the URL into **Paste redirect URL or code if not redirected automatically**. Submit it while the sign-in session is still active.
5. Select a supported Codex model, save the settings, and generate a presentation to verify the connection.

The redirect URL contains a temporary authorization code. Keep it private and do not put it in logs, documentation, or messages. If the code or session expires, start sign-in again and use the new redirect URL.
