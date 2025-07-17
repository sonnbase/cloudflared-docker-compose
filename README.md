# Cloudflare Tunnel Docker Compose

[![Docker Pulls](https://img.shields.io/docker/pulls/cloudflare/cloudflared)](https://hub.docker.com/r/cloudflare/cloudflared)
[![GitHub issues](https://img.shields.io/github/issues/sonnbase/cloudflared-docker-compose)](https://github.com/sonnbase/cloudflared-docker-compose/issues)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

## Table of Contents
- [Quick Start](#quick-start)
- [Configuration](#configuration)
- [Environment Variables](#environment-variables)
- [Usage Examples](#usage-examples)
- [Updating](#updating)
- [Security](#security)
- [Contributing](#contributing)
- [License](#license)
- [References](#references)

## Quick Start

1. **Clone this repository:**
   ```bash
   git clone <your-repo-url>
   cd <your-folder>
   ```
2. **Copy the example environment file and fill in your token:**
   ```bash
   cp .env.example .env
   # Edit .env and add your Cloudflare Tunnel token
   ```
3. **Start the service:**
   ```bash
   docker compose up -d
   ```
4. **Check logs:**
   ```bash
   docker compose logs -f cloudflared
   ```
5. **Stop the service:**
   ```bash
   docker compose down
   ```

## Configuration

- The container is named `cloudflared` for easy management.
- The restart policy is set to `always` for high availability.
- The token is securely injected via environment variable.
- You can mount a custom config file or volume if needed (see Advanced Usage).

## Environment Variables

| Variable           | Description                        |
|--------------------|------------------------------------|
| CLOUDFLARED_TOKEN  | Your Cloudflare Tunnel token       |

## Usage Examples

### Basic Usage
See Quick Start above.

### Advanced: Custom Config File
To use a custom `config.yml` for cloudflared, add a volume:
```yaml
services:
  cloudflared:
    # ...
    volumes:
      - ./config.yml:/etc/cloudflared/config.yml:ro
```

### Advanced: Docker Labels
Add labels for management or monitoring:
```yaml
services:
  cloudflared:
    # ...
    labels:
      - "com.example.description=Cloudflare Tunnel"
```

## Updating

To update to the latest image:
```bash
docker compose pull
```
Then restart:
```bash
docker compose up -d
```

## Security
- **Keep your token secure:** Use environment variables or a `.env` file. Never hardcode secrets in your compose file.
- **Rotate tokens regularly** and remove unused ones from your Cloudflare dashboard.
- **Update images regularly** to get security patches.
- **Do not expose unnecessary ports.**
- **Monitor logs** for suspicious activity.

## Contributing
See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.
- Fork the repo and create a feature branch.
- Open a pull request with a clear description.
- Use the issue tracker for bugs and feature requests.

## License
MIT. See [LICENSE](LICENSE).

## References
- [Cloudflare Tunnel Documentation](https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/)
- [cloudflared Docker Hub](https://hub.docker.com/r/cloudflare/cloudflared)
- [container-cloudflare-tunnel (inspiration)](https://github.com/jonas-merkle/container-cloudflare-tunnel) 