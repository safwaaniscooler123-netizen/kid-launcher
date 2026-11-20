# Kid Zone

A locked-down, kid-friendly launcher for macOS, shipped as **one script** (`kid.sh`).
It builds a small native kiosk app, starts it at login, and keeps kids inside a safe browser plus a set of learning apps. Only a parent (or teacher) password lets anyone leave.

**Current version: 1.2 beta-2** (the main release, the newest non-beta, is 1.1.2.2)

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

- **Parent mode (home):** kid accounts (PIN, password, pattern or none), daily screen-time limit with automatic shutdown, bedtime, breaks, weekend limits, "Open apps" timed by the parent.
- **Teacher mode (school computer):** student name sign-in (optional class roster), school-only sites, no shutdown timer, announcements, lesson link, class timer, test mode, "eyes on me" lock, hall pass, raise hand, hand-in folder and class reports. Laptops can also be paired with the web **teacher dashboard** (`teacher.html`) to control a whole class remotely, including viewing a student's Kid Zone screen.

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

## 1.2 beta-2 (beta)

Based on 1.2 beta-1. Betas are never installed automatically.

- **"Keep students on this site" now works.** Sending a lesson link from the teacher dashboard opens it on every selected laptop right away. With the lock on, a student who ends up on another page is sent back within about 2 seconds, and the Home button goes to the lesson.
- **View a student's screen.** Each laptop in the dashboard has a "View screen" button that shows the Kid Zone browser page, refreshed every 2 seconds. It only shows the Kid Zone window, not other apps. The student sees a "Your teacher is viewing this screen" notice when viewing starts, and it stops when the teacher closes the viewer.
- **More dashboard controls:** lock with your own message, go to the home page, reload the page, ding, mute and unmute, turn learning games, search, Google Images, camera and files on or off, and switch homework mode on or off.
- New `teacher.html` for the dashboard. The Supabase project needs the updated `kz_send_command` function (adds `reload`, `mute`, `unmute`).

## 1.2 beta-1 (beta)

Based on 1.1.2.2. Betas are never installed automatically.

- **New look for the Parent menu and prompts.** The parent menu, password prompts, birthday, delete account, sign-in history and the short-bedtime warning use the Kid Zone look (gradient, rounded colorful tabs, white cards) instead of native Mac dialogs. Esc always closes them, and if one fails to load it closes itself after 8 seconds. A few rarely used native alerts may remain.
- **Safer builds.** The app is compiled from a private copy and only one setup can run at a time (fixes "main.swift was modified during the build").
- **Updates in Settings.** A **Check for updates** button and an **Update automatically** checkbox (launcher Settings > Updates tile, parent password needed), with a full-screen "Getting ready for more fun!" progress screen.
- **Put config in Settings.** Settings > Websites builds a configuration profile from Kid Zone's allowed websites for Apple's web filter and opens it for approval, instead of asking each time.
- **Allow a website without a start-page tile.** The "Allow a website" dialog and Settings > Websites now have a "Don't show it on the start page" checkbox. The site is still allowed; it just does not get a tile under "Added by your grown-up".
- **Beta updates, parent password only.** The Updates tile in the launcher Settings has an **Include beta versions** checkbox. Turning it on asks for the parent password, and installing a beta asks for it again. Automatic updates only ever install stable versions.
- **Apple web filter option is off by default.** Tick "Turn on the Apple web filter option" before "Put config in Settings" works; the button also warns that the profile covers every account on the Mac.
- The script is called `kid.sh` everywhere (the old `kidzone.sh` name is gone from the help text).

## 1.1.2.2 (main release)

- **Photos can always be closed.** The video player no longer has full-screen or picture-in-picture buttons (they could trap the screen), Esc closes it, and the Close button is bigger. The picture viewer now closes from a ✖ in the top-right corner, from a click on the dark background, from the Close button, or with Esc.

## 1.1.2.1

- **Birthday is required** when a kid account is created (ages 3 to 18 only). The Parent menu "Set a kid's birthday" follows the same rule.
- **Age limits.** What a kid can open depends on their age: ages 3 to 7 each get fewer website groups and app categories and no search; age 8 has a few limits; age 9 and up get everything. Blocked below 9: Google Slides, TeachHub, Coolmath Games, Math Playground, Writer and the Brain Games apps. Blocked sites are refused by the browser, not just hidden. Parent mode with no kid signed in, and Teacher mode, are not limited.
- **More bedtimes:** 6 PM, 11 PM and 12 AM starts (all end at 7 AM), with a warning when the bedtime leaves less than 9 hours of sleep.
- **Fixed:** the greeting and birthday banner now always use the signed-in kid's name, not the name typed in Settings.

## 1.1.2
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

## Known ways around it (and why Kid Zone can't fix them)

Kid Zone is an ordinary app that runs as the signed-in user and starts at login. Anything that happens before login, or outside that account, is out of its reach:

- **Safe Mode.** Safe Mode skips login items and launch agents, so Kid Zone does not start. The kid lands on the normal desktop. (Intel: hold Shift at startup. Apple Silicon: hold the power button, pick the disk, Shift-click "Continue in Safe Mode".)
- **Recovery mode and other accounts.** These run before or outside the kid's account.
- **An admin kid account.** An admin can remove the launcher or change system settings.

Why it can't be fixed inside Kid Zone: an app cannot control a Mac that has not loaded it yet, and macOS does not let a normal app block Safe Mode or Recovery. That is a hardware and system setting, not something a script can switch off.

What helps (set in macOS, not in Kid Zone):

1. Make the kid's account a **standard (non-admin)** user and keep the admin password to yourself. This matters most.
2. **Intel Macs:** set a firmware password (blocks Safe Mode and Recovery at startup). Apple Silicon has no firmware password, but Recovery needs an admin login.
3. Turn on **FileVault** so a password is needed before Safe Mode starts.
4. Keep Apple's **Screen Time** and Content & Privacy limits on as a second layer. They are enforced by macOS itself, not by Kid Zone, so they should still apply if the kid gets into Safe Mode. This has not been tested, so check it on your own Mac.

## Last resort: block every other app with Apple's Screen Time

**Only use this as a last resort.** It is an extra layer for the case where a kid gets out of Kid Zone (for example through Safe Mode) and you want every other app on their account to stop working. It is done in macOS, not in Kid Zone, and menu names can differ a little between macOS versions.

1. Sign in to the **kid's account**. System Settings > **Screen Time** > turn it on.
2. Open **App Limits** and turn them on. Press **Add Limit** (the + button).
3. Tick every **category**, **except Kid Zone**. For the **Other** category, expand it and tick **every app except Kid Zone**.
4. Set the time to **1 minute** and turn on **Block at End of Limit**.
5. Set a Screen Time passcode so the kid cannot change it.

**Very important: never include Kid Zone in the limit.** If Kid Zone is blocked, the launcher stops opening and the kid account is stuck, so double-check the list before you save. If it does happen, a parent can remove the limit from Screen Time (or from an admin account).

Things to know:
- Each limited app only works for about 1 minute a day, then it is blocked. That includes anything you open in Kid Zone's "Open apps" mode.
- Some system apps (like Finder and System Settings) cannot be limited by Screen Time.
- Apps installed later are not in the list, so check it again after installing something.
- Screen Time cannot stop anyone from booting into Safe Mode or Recovery. The limits should still apply once the kid is there (untested), and the earlier steps in this section are what make Safe Mode hard to reach.

## Questions and answers

**Can a kid get around Kid Zone?**
Yes, in the ways listed above, mostly by booting into Safe Mode or Recovery. Using a standard account and a firmware password closes the biggest gaps. These steps have not been tested on a Mac here.

**Why can't Kid Zone block Safe Mode?**
It is a normal app that starts after login. Safe Mode is chosen before login, and macOS gives apps no way to disable it.

**What happens if the kid force-quits or closes it?**
Cmd+Tab, Cmd+Q and Force Quit are disabled, and a supervisor plus a LaunchAgent restart it if it dies. Only the parent password exits it.

**Does it work without an internet connection?**
The launcher, built-in games and apps work offline. The websites need internet.

**What if I forget the parent password?**
Run `./kid.sh --reset-password`, which needs the old password. If it is lost, you can remove Kid Zone from an admin account and reinstall.

**Will updating delete my password and settings?**
No. `./kid.sh -update` and `-reinstall` keep your password, settings and accounts.

**Can I go back to an older version?**
Yes: `./kid.sh -downgrade` asks for the parent password, shows a warning, then lets you pick any version.

**Which Macs work?**
macOS 10.13 or newer, Intel or Apple Silicon. Some features turn off on older macOS versions.

**Are we going to port this to Windows?**
No, probably not. First of all, there is a LOT, and I mean a LOT, of ways to bypass this. Secondly, personally, I HATE WINDOWS BECAUSE OF BLOATWARE AND COPILOT. If someone wants to port this, you can, but I'm never going to add it to the main repo.

**How do I allow one more website?**
Parent menu > "Allow a website" (or Settings > Websites). Type a domain like `example.com`; its subdomains are allowed too. Tick "Don't show it on the start page" if you want it allowed without a tile.

**What does a kid's birthday change?**
A birthday (ages 3 to 18) is required when an account is created. Ages 3 to 7 each get fewer website groups and app categories and no search, age 8 has a few limits, and ages 9 and up get everything, including Google Slides, TeachHub and the Brain Games apps. Blocked sites are refused by the browser, not just hidden. The full table is in the 1.1.2.1 notes above.

**What is Teacher mode?**
It turns the Mac into a school computer: students sign in with their name, only school sites open, and there is no shutdown timer. The teacher gets announcements, a lesson link, a class timer, test mode, hall passes, raised hands, a hand-in folder and reports. You choose it the first time you use it.

**How do screen time and bedtime work?**
Set a daily limit in the Parent menu. Kid Zone warns at 5 minutes and 1 minute left, then shuts the Mac down at zero. Bedtime can start at 6, 7, 8, 9, 10 or 11 PM or 12 AM and always ends at 7 AM. You get a warning if the bedtime leaves less than 9 hours of sleep, and you can still keep it.

**What is "Open apps"?**
A parent can unlock every app except Terminal and other command-line tools for 15 minutes to 2 hours. When time runs out, or the apps are closed, Kid Zone comes back.

**Does Kid Zone send my child's data anywhere?**
Kid Zone has no analytics. The only cloud part is the optional teacher dashboard: if you pair a laptop with it, that laptop sends its status (name, signed-in student, current site, time used, battery) to your own Supabase project, and screenshots of the Kid Zone window only while a teacher has the viewer open. Unpaired laptops send nothing. Settings, accounts and logs stay on the Mac (in `~/.kidlauncher` and `~/Kid Zone`). Otherwise the only network use is the websites your child opens, plus `-update` and `-downgrade`, which fetch releases from GitHub.

**How do I remove it?**
Run `./kid.sh --uninstall`. It asks for the parent password, then removes Kid Zone and its autostart.

**Can I set it up on another Mac?**
Yes. `./kid.sh --usb` puts an installer on a USB stick that sets Kid Zone up on another Mac.

**Why does the first run take a while?**
Kid Zone builds its app on your Mac the first time, and it needs the free Xcode Command Line Tools. The script offers to install them. If the build fails, read `~/.kidlauncher/build.log`.

**What is the difference between using "Open apps" and "Exit Kid Zone"?**
"Open apps" is a temporary, supervised unlock. "Exit Kid Zone" turns Kid Zone off.

| | Open apps | Exit Kid Zone |
|---|---|---|
| Kid Zone | Stays running in the background with a countdown | Quits completely |
| Which apps | Everything except Terminal and other command-line tools (they are closed on sight) | Everything, including Terminal |
| How long | 15 minutes to 2 hours, then Kid Zone comes back by itself | Until someone starts Kid Zone again or the next login |
| Ends early | When the apps are closed, or the kid presses Done | Never ends by itself |
| Screen-time clock and bedtime | Keep running, and shut the Mac down if they run out | Stopped, so no screen-time limit or bedtime shutdown |
| Apps left open at the end | Closed for you | Left open |
| Logging | Recorded in the activity log | Only the exit is logged |

Use "Open apps" when your child needs another app for a while (for example, a school program). Use "Exit Kid Zone" when a grown-up wants to use the Mac normally. Both ask for the parent password. After "Exit Kid Zone", Kid Zone is not restarted automatically, but it starts again at the next login.

**What if a kid gets out of Kid Zone and I want to block every other app?**
As a last resort, use Apple's Screen Time App Limits on the kid's account: limit every category and every app in "Other" to 1 minute, except Kid Zone. Never include Kid Zone, or the launcher will stop opening. The steps are in "Last resort: block every other app with Apple's Screen Time" above.

**I use Apple's Screen Time web limits, then allowed a website in Kid Zone, and it is still blocked. How do I fix it?**
There are two separate allow-lists: Kid Zone's own, and Apple's Content & Privacy list that macOS enforces on top. Kid Zone cannot edit Apple's Screen Time list (it is protected by macOS and your Screen Time passcode). Instead, tick **Settings > Websites > Turn on the Apple web filter option** (it is off by default), then press **Put config in Settings** and confirm the warning. Kid Zone builds an Apple configuration profile from everything it allows and opens it; you approve it in System Settings (Privacy & Security > Profiles) with an admin password. After you allow a new site, press the button again to refresh it.
Things to know first:
- The profile is a web content filter that applies to **every account on this Mac**, including yours, not just the kid's. To remove it, select it under Profiles and press the minus button.
- Set Apple's own web setting back to Unrestricted or "Limit Adult Websites" so the two lists do not fight.
- It is built from Apple's documented web content filter profile for macOS 10.15 and later. It has not been tested on a Mac here, so try it on a spare account first.
- The simplest option is not to use Apple's "Only Approved Websites" at all, because Kid Zone already blocks everything that is not on its list.

**How do updates work inside Kid Zone?**
The launcher Settings has an **Updates** tile (parent password needed) with a **Check for updates** button and an **Update automatically** checkbox (on by default). Kid Zone checks GitHub shortly after it starts and every 6 hours, only for the newest non-beta version. When it updates, a "Getting ready for more fun!" screen with a progress bar covers the Kid Zone while it downloads, builds and restarts. Your password, accounts and settings are kept. If the build fails, the old version keeps working and a message explains why. Auto updates are skipped in Teacher mode and while apps are unlocked. Kid Zone keeps its own copy of `kid.sh` in `~/.kidlauncher` for this; your original `kid.sh` is not changed, so `./kid.sh -update` still works for that file.

## Honest notes

- The Swift code compiles on your Mac when you run the script. If it fails, read `~/.kidlauncher/build.log`.
- macOS asks for camera and microphone permission the first time (and may ask again after a rebuild).
- A determined adult can always leave with the parent password; kids cannot.
