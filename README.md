# Cloudflare Tunnel with Docker Compose

This project provides a simple way to run a Cloudflare Tunnel using Docker Compose. It securely exposes your local or internal services to the internet via Cloudflare's network.

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/) installed
- [Docker Compose](https://docs.docker.com/compose/install/) installed
- A Cloudflare account
- A Cloudflare Tunnel token ([how to get one](https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/create-tunnel/))

## Setup Instructions

1. **Clone this repository or copy the files to your server:**
   ```bash
   git clone <your-repo-url>
   cd <your-folder>
   ```

2. **Create a `.env` file:**
   In the project directory, create a file named `.env` and add your Cloudflare Tunnel token:
   ```env
   CLOUDFLARED_TOKEN=your_cloudflare_tunnel_token_here
   ```
   > **Tip:** Never commit your `.env` file to version control. It contains sensitive credentials.

3. **Review and customize `docker-compose.yml` if needed:**
   - The container is named `cloudflared` for easy management.
   - The restart policy is set to `always` to ensure high availability.
   - The token is securely injected via environment variable.

4. **Start the service:**
   ```bash
   docker compose up -d
   ```
   This will pull the latest `cloudflare/cloudflared` image and start the tunnel.

5. **Check logs:**
   ```bash
   docker compose logs -f cloudflared
   ```

6. **Stop the service:**
   ```bash
   docker compose down
   ```

## Best Practices

- **Keep your token secure:**
  - Use environment variables or a `.env` file. Never hardcode secrets in your compose file.
  - Do not share your token publicly.
- **Update regularly:**
  - The image uses `latest` tag. Periodically run `docker compose pull` to get updates.
- **Monitor the tunnel:**
  - Use `docker compose logs` to monitor for errors or connection issues.
- **Use container names:**
  - The container is named `cloudflared` for easy reference in Docker commands.
- **Restart policy:**
  - The `restart: always` policy ensures the tunnel restarts automatically if it crashes or the host reboots.
- **Version control:**
  - Exclude `.env` from your version control system (add it to `.gitignore`).

## Troubleshooting

- **Tunnel not connecting?**
  - Double-check your token in the `.env` file.
  - Check your internet connection and firewall settings.
- **Logs show errors?**
  - Use `docker compose logs -f cloudflared` to view real-time logs.
- **Need to update the token?**
  - Edit the `.env` file and restart the service: `docker compose down && docker compose up -d`

## References
- [Cloudflare Tunnel Documentation](https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/)
- [cloudflared Docker Hub](https://hub.docker.com/r/cloudflare/cloudflared)

---

**Security Reminder:**
- Never share your Cloudflare Tunnel token.
- Always use environment variables for secrets.
- Regularly update your images and monitor logs for suspicious activity. 