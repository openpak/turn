# Deploy

- Quadlet: `deploy/openpak-turn.container` (host network, `Exec=-c /etc/turnserver.conf`).
- Config: `~/openpak/deploy/turn/turnserver.conf` on the box, from `deploy/turnserver.conf.example`.
  The secret must equal `NPLN_TURN_SECRET` in `deploy/.env`, which `connectivity` uses to sign credentials.
- Firewall: UDP 3478 and 49152-65535 open on the host and the cloud security list.
- Restarting drops active relays; check `journalctl --user -u openpak-turn` for recent allocations first.
- Release: push a `v*.*.*` tag; CI publishes `ghcr.io/openpak/turn:X.Y.Z` and `:latest` for amd64 and arm64.
