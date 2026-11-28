# Keeping data on the user's machine and sharing it

Date: 28 November 2026. The question: data stays on each person's machine and a hosted server keeps only accounts and
what sharing needs ([vision](../vision.md)); how do other projects share a document kept on one device?

Clones in `.tmp/`: excalidraw `f4e5226` (2026-11-27), excalidraw-room `03ff435` (2023-12-15), any-sync `76a618a`
(2026-11-27), any-sync-dockercompose `960805a` (2026-10-23).

## Zalo

From press coverage, not Zalo's own documentation:

- The phone app and Zalo PC keep message history on the device; moving history to a new device needs a backup made
  beforehand, and syncing to a PC needs the phone to approve it
  ([Điện Máy Xanh](https://www.dienmayxanh.com/kinh-nghiem-hay/cach-dong-bo-tin-nhan-zalo-tren-dien-thoai-va-may-1126184)).
- Since late April 2025 Zalo Web keeps messages for 14 days from the first login in a browser
  ([Dân Trí](https://dantri.com.vn/cong-nghe/zalo-gay-tranh-cai-vi-gioi-han-so-ngay-luu-tru-tin-nhan-tren-web-20250513153033601.htm)).

## Excalidraw: an encrypted snapshot behind a link

- `exportToBackend` (`excalidraw-app/data/index.ts:248`) generates an AES-GCM key in the browser
  (`packages/excalidraw/data/encryption.ts`), compresses and encrypts the drawing, and posts the bytes to a JSON store
  (`VITE_APP_BACKEND_V2_POST_URL=https://json.excalidraw.com/api/v2/post/` in `.env.production`).
- The share link is `#json=<id>,<key>`. The comment in the code: "We need to store the key (and less importantly the
  id) as hash instead of queryParam in order to never send it to the server". The server keeps bytes it cannot read.
- The snapshot is a copy: later edits by the author do not reach it until a new link is made.

## excalidraw-room: a relay for people online at the same time

- `src/index.ts` is a Socket.IO server with `join-room`, `server-broadcast` and `server-volatile-broadcast`; it
  forwards `encryptedData` and `iv` to the other sockets of the room and stores nothing.
- People see each other's changes only while connected.

## any-sync (Anytype): encrypted sync nodes

- README: spaces are "End-to-end encrypted", data is "stored as encrypted Directed Acyclic Graphs", changes merge as
  a CRDT; "Providers cannot read user information".
- Self-hosting it (`any-sync-dockercompose/docker-compose.yml`) runs a sync node, a coordinator, a file node, a
  consensus node, MongoDB, Redis and an S3 store (Garage or MinIO).

## Obsidian and Logseq

- Obsidian keeps a vault as files on the device. Obsidian Sync, the paid service, is end-to-end encrypted
  ([help](https://obsidian.md/help/sync/security)); the community plugin
  [Self-hosted LiveSync](https://github.com/vrtmrz/obsidian-livesync) syncs through the user's own CouchDB or S3
  store, also encrypted. Neither was read in code.
- Logseq Sync is closed source; Logseq's April 2026 changelog added custom sync server URLs
  ([forum](https://discuss.logseq.com/t/whats-new-with-logseq-db-april-26-2026/34977)). Not read in code.

## Patterns

| Pattern | Seen in | What the server keeps | A friend sees a topic while its owner's machine is off | Moving parts on the server |
| --- | --- | --- | --- | --- |
| Encrypted snapshot | Excalidraw share links | encrypted copies of shared items | yes, the last copy uploaded | one store of blobs |
| Relay only | excalidraw-room | nothing | no | one socket server |
| Encrypted sync of everything | any-sync, Obsidian Sync, LiveSync | encrypted copies of all data, every change | yes, up to date | several services (any-sync: seven containers) |
