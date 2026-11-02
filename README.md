# turn

OpenPak's STUN/TURN relay for NPLN titles.

| | |
| --- | --- |
| Network | all (used by Switch NPLN titles and the shared connectivity service) |
| Role | TURN relay, UDP 3478 plus the 49152-65535 relay range, host network |
| Depends on | nothing; `connectivity` issues the HMAC credentials from the same secret |
| Image | `ghcr.io/openpak/turn` |
| Based on | [coturn](https://github.com/coturn/coturn) at commit `176ce42`, two interoperability patches applied at build time (see `Dockerfile`) |
| Licence | AGPL-3.0-only for this repository; coturn is BSD-3-Clause |

## What it does

Nintendo's Pia TURN client writes method attributes after `MESSAGE-INTEGRITY`, which stock
coturn ignores since RFC 8489 handling landed. The two patches in the `Dockerfile` read those
attributes again and default `ALLOCATE` to UDP when `REQUESTED-TRANSPORT` is missing. Without
them every Pia `CHANNEL-BIND` fails with 400 and no relay forms.

## Run

The quadlet in `deploy/` runs the image on the host network with `-c /etc/turnserver.conf`.
Copy `deploy/turnserver.conf.example`, set the secret and public address, and mount it read-only.

## Docs

- [Protocol](docs/protocol.md)
- [Deploy](docs/deploy.md)
- [Provenance](docs/provenance.md)
