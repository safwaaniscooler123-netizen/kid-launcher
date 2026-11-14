# Kid Zone

A locked-down, kid-friendly launcher for macOS, shipped as **one script** (`kid.sh`).
It builds a small native kiosk app, starts it at login, and keeps kids inside a safe browser plus a set of learning apps. Only a parent (or teacher) password lets anyone leave.

**Current version: 1.1.2.1**

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
| `./kid.sh -update` | Check GitHub for the newest version (no betas) and offer to install it |
| `./kid.sh -updatebeta` | Same, but beta versions count too |
| `./kid.sh -downgrade` | Asks for the parent password, shows a warning, then lets you pick any version (betas too) to install |
| `./kid.sh --reset-password` | Change the parent password |
| `./kid.sh --usage` | Today's screen time and the activity log |
| `./kid.sh --version` | Print the version |
| `./kid.sh --uninstall` | Remove Kid Zone and its autostart |

## Two modes

- **Parent mode (home):** kid accounts (PIN, password, pattern or none; a birthday is required), daily screen-time limit with automatic shutdown, bedtime, breaks, weekend limits, "Open apps" timed by the parent.
- **Teacher mode (school computer):** student name sign-in (optional class roster), school-only sites, no shutdown timer, announcements, lesson link, class timer, test mode, "eyes on me" lock, hall pass, raise hand, hand-in folder and class reports.

## What kids get

- One browser with an address bar (website or question, strict safe search), bookmarks, reload, stop, zoom and back/forward.
- 80+ apps: quizzes and games, Book Log, Files, Photos, Camera (3 second countdown with the Photo Booth sound, photos and video), Writer, Piano, Pixel Art and more.
- A start page with stars, favorites and a need-help button.

## Age limits (new in 1.1.2.1)

A kid account **must have a birthday** (Kid Zone accepts ages 3 to 18; anything older or younger is refused). The birthday decides what is unlocked, so older kids get more.

<table>
<thead>
<tr><th align="left">Age</th><th align="left">Website groups</th><th align="left">App categories</th><th align="left">Camera, Files, Photos</th><th align="left">Search bar and Google Images</th></tr>
</thead>
<tbody>
<tr><td>3</td><td>Watch and Play, School</td><td>My Computer, Create &amp; Play</td><td>Hidden</td><td>Off</td></tr>
<tr><td>4</td><td>+ Reading and Writing</td><td>+ Reading &amp; Writing</td><td>Hidden</td><td>Off</td></tr>
<tr><td>5</td><td>+ Math</td><td>+ Math</td><td>Shown</td><td>Off</td></tr>
<tr><td>6</td><td>+ Science and Nature</td><td>+ Science, My World</td><td>Shown</td><td>Off</td></tr>
<tr><td>7</td><td>+ Learn Anything</td><td>+ Tools</td><td>Shown</td><td>Off</td></tr>
<tr><td>8</td><td>All groups</td><td>All except Brain Games</td><td>Shown</td><td>Allowed</td></tr>
<tr><td>9 and up</td><td>All groups</td><td>All</td><td>Shown</td><td>Allowed</td></tr>
</tbody>
</table>

- Ages 3 to 7 never get the Code and Typing group. The School group is allowed for them, including Google Docs and Sheets, except Google Slides and TeachHub (blocked below age 9).
- **Blocked below age 9:** Google Slides (Docs and Sheets are allowed), TeachHub, Coolmath Games, Math Playground, the Writer app and the Brain Games apps.
- Blocked sites are refused by the browser too, not only hidden from the start page.
- Parent mode with no kid signed in, and Teacher mode, get everything. An old account with no birth year is treated as age 8; set it in Parent menu > "Set a kid's birthday".
- To change the rules, edit `kzBigKidAge`, `kzYoungBlocked` and `kzAgeBlocked` (Swift) and `YOUNG_SITES`, `AGE_SITES` and `AGE_APPS` (JavaScript) in `kid.sh`.

## What is locked

- No close, minimize or fullscreen buttons; no Dock or menu bar; Cmd+Tab, Cmd+Q and Force Quit are disabled.
- Runs detached and supervised, so Ctrl+C or closing Terminal does nothing.
- Sites outside the allow list are blocked (kids can press "Ask a grown-up").

## Files

- Kid files: `~/Kid Zone`
- Settings, logs and allow lists: `~/.kidlauncher` (`allowlist.txt`, `allowed-extra.txt`, `blocked-extra.txt`, `blocked-words.txt`, `roster.txt`)
- Backups and reports: `~/Kid Zone Backups`

## 1.1.2.1
- **Required birthday.** New kid accounts need a birthday (date picker). Ages 3 to 18 only. The Parent menu birthday dialog follows the same rule.
- **Age limits.** Ages 3, 4, 5, 6 and 7 each have their own limits, age 8 has a few, and 9 and up get everything (see the table above). The School group is available to ages 3 to 7 too.
- **More bedtimes.** 6 PM, 11 PM and 12 AM starts (all end at 7 AM) join 7, 8, 9 and 10 PM in the Parent menu and Settings. A **sleep warning** appears if the bedtime leaves less than 9 hours (11 PM and 12 AM); a parent can still keep it.
- **Wrong name fixed.** The greeting, birthday banner and top bar now use the kid who is signed in. Before, a name a parent had typed in Settings (for example "Ava") could show for a different kid (for example "Sofia").
- See `RELEASE_NOTES.md`.

## 1.1.2 (main release)
- **The Parent menu "More" tab is organized** into sections: Accounts, Safety and access, Data and checks, Power (and Class in Teacher mode).
- **Autocorrect is off** in the address bar, in Kid Zone's own text boxes and on every web page (no spell-check underlines, smart quotes or text replacement).
- **No Cut in the address bar's right-click menu** (Copy and Paste stay).
- **Updates:** run `./kid.sh -update` in Terminal. It checks GitHub for the newest release, compares it with your version, and offers to install it (password and settings are kept), replaces your kid.sh file with the new version and makes it executable (chmod +x). Betas are left out; use `./kid.sh -updatebeta` to include them.
- **Downgrade:** `./kid.sh -downgrade` asks for the parent password, shows a warning (you must type YES), lists every GitHub version, and installs the one you pick. Your kid.sh is replaced with that version.

## 1.1.1.0.1 (bug fix)
- No more "boop" sound when you hold a key down in a game.
- Snippet fixes (typing works again after Esc, the saved area always matches your selection), clearer Sticky Keys ON/OFF message, and held arrow keys still scroll pages.

## 1.1.1
- **Copy and Paste** work (Cmd+C, Cmd+V, Cmd+A) in text boxes, the address bar and web pages. There is **no Cut**.
- **macOS screenshots are blocked.** Cmd+Shift+3, 4, 5 and 6 do nothing (needs the Accessibility permission, same as the volume keys).
- **Kid Zone snippet:** press Option+Cmd+Shift+S, drag over the part of the page you want, and the picture is saved in Photos. Needs the Files app turned on by a parent.
- **Video snippets:** Option+Cmd+Shift+V, drag over the page, and it records that part (1 minute max). Press the keys again to stop. Saved in Photos.
- **No snipping in Google Meet or Zoom** (a recording in progress stops and is deleted if the page changes to one of them).
- **Sticky Keys:** Shift five times turns it on (or use the Parent menu). Tap a modifier key once to hold it, twice to lock it, a third time to release it.
- See `RELEASE_NOTES.md` for this version.

## 1.1
- **Your rocket icon** is the app icon.
- **Installed in Applications.** After running the script once, open **Kid Zone** from your Applications folder (or `~/Applications`). No Terminal needed. Opening it twice just uses the one that is running.
- **Birthdays.** Parent menu > "Set a kid's birthday". When that kid signs in on their birthday, Kid Zone celebrates with confetti, a song, a banner and 3 bonus stars (once a day).
- **Old-style volume pop-up** also appears when the keys can't be intercepted yet (before Accessibility is allowed).

## Earlier 1.1 updates
- **Real app bundle.** Kid Zone is now built as a signed `KidZone.app` inside `~/.kidlauncher`, so macOS can finally show the Location prompt. After the first launch, allow Location in System Settings > Privacy & Security.
- **Accessibility prompt** is asked once, then checked quietly. A rebuild clears the old stale permission row so you allow it once.
- **Wi-Fi**: "Saved networks" and "Join by name" (no Location access needed).
- **Volume keys**: hold Shift or Option for tiny steps. The macOS pop-up never shows.
- **Settings**: 28 groups of 20 settings (26 look-and-feel groups, Wallpaper with pictures, Screensaver with videos) plus the 50 basic settings.
- **Zoom** is allowed (camera and microphone too, if the camera is on).
- **20 games** (not educational) unlock at 10 stars each day.

## 1.1 changes

- Fixed the purple screen: it came from the **Night / Auto theme**, which was deep purple (Auto switches to it after 7pm). Night is now dark blue with readable cards. Launch is also protected against a blank start page (the window is no longer purple, the page reloads itself if it does not appear, and page errors are written to `usage.log`).
- Image wallpaper and a video screensaver (Settings > Wallpaper and screensaver).
- Old-style gray volume and brightness pop-up. The keyboard volume/brightness keys are handled by Kid Zone and the modern macOS pop-up is hidden. This needs the **Accessibility** permission (macOS asks once); brightness uses a private Apple API.
- Wi-Fi menu (📶) and Control Center (🎛) in the top bar. Changing the network or turning Wi-Fi off needs the parent password.
- Websites a parent adds ("Allow a website") now show on the start page. Google Meet is allowed (camera and microphone only for meet.google.com).
- 10 new apps: Breathing Buddy, Joke Box, Sticker Book, Silly Stories, Thankful Journal, Typing Race, Kindness Cards, Daily Challenge, Countdown, and a "More time?" request button.

## 1.1-beta-1 changes

- **Settings app with 50 settings** in five groups: Look (colors, text size, font, corners, spacing, contrast, black and white, dimming, background, tile size, emoji), Easier to use, Sound and voice, Start page, Learning and apps.
- **Google Images with SafeSearch forced on.** A parent turns it on in the Parent menu ("Google Images + save pictures"). The 🖼 button searches for pictures; the ⬇ button saves the biggest picture on screen into `~/Kid Zone/Downloads` (shown in Photos and Files). Only image pages of Google are opened, nothing else on google.com.
- **Camera Background Swap** (Settings > Camera background): pick a picture and the Camera finds you in each frame and puts the picture behind you, for photos and videos. Uses Apple's Vision person segmentation, so it needs macOS 12 or newer.

## 1.0.2 changes

- Build fix (account helpers were missing).
- Escalating sign-in lockouts: 30 seconds, 1 minute, 5 minutes, 15 minutes, 30 minutes, then 1 hour after every 5 wrong tries. Saved on disk so a restart does not reset it; a parent can clear it from the menu.

## 1.0 (first release)

- 25 essential features in one script, with one consistent button style.

## 1.0 beta

- 27 kid-safe websites in groups on the home screen (YouTube Kids, Simple English Wikipedia, Cool Math 4 Kids, Coolmath Games, Matific, IXL, TeachHub and more), kept in one editable table that feeds the tiles and the allow list.
- 10 learning games plus 6 built-in public-domain tunes (the 🎵 button cycles them).
- One big browser with an address bar (safe search), reload, bookmarks and "Ask a grown-up" on blocked sites.
- Files app (`~/Kid Zone`), Photos app, Camera app (3 second countdown, photos and video).
- Teacher mode: student sign-in, school-only sites, announcements, lesson link, class timer, test mode, hall pass, raise hand, hand-in folder and reports.
- 80+ apps in one Apps screen (Book Log, calculator, drawing pad, notes, to-do list, times tables and more).
- Parent tools: weekend limit, pause the clock, volume cap, homework mode, games on/off, note to the child, activity log viewer, allow a website, YouTube Kids setup.
- Shutdown, restart and volume done in Swift (no osascript); Restart button; closes the "Open apps, Dock, remove the launcher" loophole; launcher files flagged immutable.

## 1.0 alpha

- First working version: YouTube Kids, Simple English Wikipedia and Cool Math 4 Kids (only these).
- Two learning games: Pizza Fractions and Cupcake Bakery.
- Kiosk lock: no close, minimize or fullscreen buttons, no Dock or menu bar; Cmd+Tab, Cmd+Q, Force Quit and Hide disabled.
- Parent password (salted PBKDF2), parent menu, daily screen-time limit with shutdown, Open apps mode, activity log.
- Auto-restart if killed, starts at login, `-reinstall` and `--uninstall`.

## Honest notes

- The Swift code compiles on your Mac when you run the script. If it fails, read `~/.kidlauncher/build.log`.
- macOS asks for camera and microphone permission the first time (and may ask again after a rebuild).
- A determined adult can always leave with the parent password; kids cannot.
