# The Long Couch

Watch videos together with friends, wherever they are. Open a room, paste a link to a video file and share the room link: everyone's playback stays in sync, so play, pause and seek happen for everyone at the same time.

**Try it: [the-long-couch.rodlabs.dev](https://the-long-couch.rodlabs.dev)**

> Formerly called *Movie Night*. That name now belongs to a [different project](https://github.com/rodrigohpalmeirim/movie-night).

## Features

- **Rooms by link**: opening the site creates a room with a random ID in the URL. Copy the link and send it to friends, who see how many people are in the room and the video's duration before they join.
- **Synchronized playback**: play, pause and seek are broadcast to everyone in the room. People who join late start at the current position.
- **Buffering-aware**: when someone seeks or their stream stalls, playback waits until everyone has buffered ("Waiting for N people's stream...") and then resumes for all.
- **Any direct video URL**: the video plays in the browser's native `<video>` player from any URL it can stream (e.g. an `.mp4` link). Each viewer streams it themselves, so the server never handles video.
- **Subtitles**: upload `.vtt` or `.srt` files (SRT is converted to WebVTT in the browser). They're shared with everyone in the room, including people who join later.
- **Reconnects**: a client that loses its connection rejoins the room on its own.
- Fullscreen toggle, controls that hide automatically, and a debug log you can download by pressing `l`.

## How it works

- **Client** (`client/`): a React app (Create React App) built with React hooks and Font Awesome icons.
- **Server** (`server/index.js`): a Node.js [Express](https://expressjs.com) server that serves the built client and runs a [Socket.IO](https://socket.io) server. It keeps the state of each room in memory (URL, subtitles, play/pause state, last known position, number of people, how many are still buffering) and relays playback events between clients.

The first version (2020) was peer-to-peer with PeerJS and deployed to GitHub Pages. In December 2021 it was rewritten around a central Socket.IO server.

## Running locally

Requires Node.js and npm.

```sh
git clone https://github.com/rodrigohpalmeirim/the-long-couch.git
cd the-long-couch
npm install

# Build the client and start the server
npm run build
npm start          # http://localhost:5000 (set PORT to change)
```

### Development

Run the server and the React dev server side by side. The dev server proxies requests to the server on port 5000:

```sh
npm start                 # server on :5000
cd client && npm install && npm start    # client on :3000 with hot reload
```

## License

[GPL-3.0-or-later](LICENSE)
