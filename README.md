# Breach Sandbox

A simulated hacker-terminal toy that runs entirely in the browser — a fake
filesystem, a brute-force password cracker, a lockable root account. It's a
game, not a tool: there's no backend, no network calls, and nothing it
touches is real.

**[Live demo](https://claude.ai/artifact/TrXd32c5gg5cMGcL7Muqd2)**

## How it works

Open `index.html` (or the live demo above) and type `help` in the terminal.
See [`HACKS.md`](./HACKS.md) for the full command list and the intended
exploit chain.

## Why it's safe

- Pure static HTML/CSS/JS — one file, no build step, no server.
- All "hacking" is a simulated in-memory filesystem; nothing leaves the
  browser tab.
- State is never persisted (no `localStorage`/cookies/backend), so closing
  the tab or hitting the in-page **reboot** button wipes everything back to
  a clean boot.

## Run it locally

```bash
git clone <this-repo>
cd breach-sandbox
python3 -m http.server 8000
# open http://localhost:8000
```

Or just open `index.html` directly in a browser — no build step needed.
