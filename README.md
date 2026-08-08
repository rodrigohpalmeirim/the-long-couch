# The Long Couch

Formerly known as Movie Night.

Watch videos together, in sync. Everyone in a room shares the same playback: play,
pause, seek, video URL and subtitles are kept in step over a socket.io connection,
and playback waits while anyone is still buffering.

## Structure

- `client/` — Svelte + Vite front end (player and controls)
- `server/` — Express + socket.io server that keeps the rooms in sync and serves
  the built client

## Development

```sh
cd server && npm install && npm run dev   # server on port 5174
cd client && npm install && npm run dev   # client dev server, proxies /socket.io
```

In production the client is built with `npm run build` in `client/`, and the
server serves the resulting `client/dist` alongside the socket connection.
