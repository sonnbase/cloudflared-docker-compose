# Advanced Configuration for Cloudflare Tunnel Docker Compose

This guide covers advanced configuration options for running cloudflared with Docker Compose, including custom configuration files, persistent storage, and Docker labels.

## 1. Using a Custom config.yml

You can provide a custom `config.yml` to cloudflared for advanced tunnel configuration (e.g., ingress rules, logging, etc.).

**Steps:**
1. Create a `config.yml` in your project directory. Example:
   ```yaml
   tunnel: <TUNNEL-UUID>
   credentials-file: /etc/cloudflared/<TUNNEL-UUID>.json
   ingress:
     - hostname: example.com
       service: http://localhost:8080
     - service: http_status:404
   ```
2. Mount the config file in your `docker-compose.yml`:
   ```yaml
   services:
     cloudflared:
       # ...
       volumes:
         - ./config.yml:/etc/cloudflared/config.yml:ro
   ```

## 2. Mounting Volumes for Persistent Storage

If you need to persist credentials or logs, mount a directory from your host:
```yaml
services:
  cloudflared:
    # ...
    volumes:
      - ./cloudflared:/etc/cloudflared
```
- Place your credentials and config files in the `cloudflared` directory on your host.

## 3. Using Docker Labels

Docker labels can help with container management, monitoring, or integration with orchestration tools:
```yaml
services:
  cloudflared:
    # ...
    labels:
      - "com.example.description=Cloudflare Tunnel"
      - "maintainer=yourname@example.com"
```

## References
- [Cloudflare Tunnel config.yml reference](https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/configuration/)
- [Docker Compose volumes](https://docs.docker.com/compose/compose-file/compose-file-v3/#volumes)
- [Docker labels](https://docs.docker.com/config/labels-custom-metadata/) 