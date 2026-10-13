# Breach Sandbox — full command / "hacks" list

Everything below runs entirely client-side against a fake in-memory filesystem.
Nothing here reaches a real network, file, or account. State resets on reboot
or page reload.

## Recon
| Command | What it does |
|---|---|
| `help` | Lists every available command |
| `ls [path]` | Lists the current (or given) directory |
| `cd <path>` | Moves into a directory (`cd ..` goes up) |
| `cat <file>` | Prints a file's contents |
| `whoami` | Shows the current user (`guest` or `root`) |
| `scan` | "Scans" the fake network and reveals the target host |
| `history` | Shows commands you've run this session |

## The exploit chain (intended order)
1. `cat notes.txt` — hints that `/root` is locked and the passphrase hash
   lives in `/root/shadow.enc`.
2. `scan` — reveals the target host and confirms `/root/shadow.enc` is the
   thing to go after.
3. `crack /root/shadow.enc` — runs a live brute-force animation that locks
   in a fake passphrase (`R00T-ACC3SS`) character by character.
4. `sudo su` — now that the passphrase is "known," elevates you to root.
5. `ls /root` / `cat /root/shadow.enc` — the vault is now readable.
6. `decrypt /root/flag.txt` — reveals the win message:
   `SANDBOX{nice_work_you_cracked_it}`

## Extras
| Command | What it does |
|---|---|
| `matrix` | Toggles the green falling-code background |
| `clear` | Clears the screen |
| `reboot` | Wipes all state and restarts from a clean boot |

## Why it's safe to publish as-is
- No `eval`, no `fetch`/network calls, no backend, no storage API used for
  game state — everything lives in a JS variable that's thrown away on
  reload.
- The one DOM sink (`innerHTML`) only ever receives hardcoded strings or
  text that's been HTML-escaped first — there's no injection path from
  anything you type into the terminal.
- The "vulnerabilities" in the sandbox (locked root, the crackable
  passphrase) are intentional game design, not real exploitable bugs —
  that's the whole point of the toy.
