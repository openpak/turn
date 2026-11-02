# Protocol

Standard STUN/TURN (RFC 5389/5766, long-term credentials via `use-auth-secret`), with two
deviations observed from Nintendo's Pia client on 2026-10-11 (Terraria, Switch and Harbor):

1. `ALLOCATE` carries `USERNAME`, `REALM`, `NONCE`, `MESSAGE-INTEGRITY`, then `REQUESTED-TRANSPORT`.
   `CHANNEL-BIND` carries the same four, then `CHANNEL-NUMBER` and `XOR-PEER-ADDRESS`.
   Attributes after `MESSAGE-INTEGRITY` must still be read. Authentication attributes are
   only looked up before it, so credentials stay integrity-covered.
2. An `ALLOCATE` without `REQUESTED-TRANSPORT` means UDP (17).

Credentials are `timestamp:user` with an HMAC-SHA1 over the shared secret; the realm is
announced by the server in the 401 challenge, so changing it does not break clients.
