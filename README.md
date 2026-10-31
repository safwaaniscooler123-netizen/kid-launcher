[README.md](https://github.com/user-attachments/files/34227441/README.md)
# Kid Zone

A locked-down, kid-friendly launcher for macOS, shipped as **one script** (`kid.sh`).
It builds a small native kiosk app, starts it at login, and keeps kids inside a safe browser plus a set of learning apps. Only a parent (or teacher) password lets anyone leave.

**Current version: 1.0.2**

## Install

```bash
git clone https://github.com/safwaaniscooler123-netizen/kid-launcher
cd kid-launcher
chmod +x kid.sh
./kid.sh
```

First run: create the parent password, choose **Parent** or **Teacher** mode, and (parent mode) set up a kid account from the Parent menu. Needs macOS with the Xcode command line tools (`xcode-select --install`) so `swiftc` can build the app.

| Command | What it does |
|---|---|
| `./kid.sh` | Start Kid Zone |
| `./kid.sh -reinstall` | Rebuild and re-register everything (keeps password and settings) |
| `./kid.sh --reset-password` | Change the parent password |
| `./kid.sh --usage` | Today's screen time and the activity log |
| `./kid.sh --version` | Print the version |
| `./kid.sh --uninstall` | Remove Kid Zone and its autostart |

## Two modes

- **Parent mode (home):** kid accounts (PIN, password, pattern or none), daily screen-time limit with automatic shutdown, bedtime, breaks, weekend limits, "Open apps" timed by the parent.
- **Teacher mode (school computer):** student name sign-in (optional class roster), school-only sites, no shutdown timer, announcements, lesson link, class timer, test mode, "eyes on me" lock, hall pass, raise hand, hand-in folder and class reports.

## What kids get

- One browser with an address bar (website or question, strict safe search), bookmarks, reload, stop, zoom and back/forward.
- 80+ apps: quizzes and games, Book Log, Files, Photos, Camera (3 second countdown with the Photo Booth sound, photos and video), Writer, Piano, Pixel Art and more.
- A start page with stars, favorites and a need-help button.

## What is locked

- No close, minimize or fullscreen buttons; no Dock or menu bar; Cmd+Tab, Cmd+Q and Force Quit are disabled.
- Runs detached and supervised, so Ctrl+C or closing Terminal does nothing.
- Sites outside the allow list are blocked (kids can press "Ask a grown-up").

## Files

- Kid files: `~/Kid Zone`
- Settings, logs and allow lists: `~/.kidlauncher` (`allowlist.txt`, `allowed-extra.txt`, `blocked-extra.txt`, `blocked-words.txt`, `roster.txt`)
- Backups and reports: `~/Kid Zone Backups`

## 1.0.2 changes

- Build fix (account helpers were missing).
- Escalating sign-in lockouts: 30 seconds, 1 minute, 5 minutes, 15 minutes, 30 minutes, then 1 hour after every 5 wrong tries. Saved on disk so a restart does not reset it; a parent can clear it from the menu.

## 1.0.1 changes

- New login screen built in the same web UI as the rest of the app (profile picker, PIN pad, password, pattern, grown-up setup).
- Battery now updates every 10 seconds and the moment the charger is plugged or unplugged.
- Address bar always matches the page.
- 25 new features: switch-user button, auto return to login after 20 idle minutes (with a warning), delete account, 5-try lockout, show/hide password, Enter key and keyboard PIN entry, sign-in history, account avatars, last-user hint, signed-in name on the start page, forward button, loading spinner, shortcuts (Cmd+L, R, [, ], +, -, 0), shortcuts listed in Help, auto night theme, parent menu entries for accounts and history, and more.

## Honest notes

- The Swift code compiles on your Mac when you run the script. If it fails, read `~/.kidlauncher/build.log`.
- macOS asks for camera and microphone permission the first time (and may ask again after a rebuild).
- A determined adult can always leave with the parent password; kids cannot.
