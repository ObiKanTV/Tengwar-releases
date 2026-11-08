# Tengwar

Maps your controllers (stick, throttle, pedals, button box, gamepad: any brand) to your games, and
writes each game's own binding file for you to use.

Tengwar shows every control on your devices with what it does in the game you pick, checks the layout
for clashes (two jobs on one button, reserved buttons, important actions left on the keyboard), and
installs the result straight into the game. It reads your controllers directly from Windows, so it
sees every button a device has (many tools stop at 32; some sticks and throttles have up to 128) and
recognises a control the moment you press it.

Tengwar is free, in early access: expect rough edges, and please [report what you find](#help-and-bug-reports).

**[Download the newest version](../../releases/latest)** · [What's new](../../releases) ·
**[First-time setup guide](guides/first-time-setup.md)**

See the [disclaimer](DISCLAIMER.md). Tengwar is not affiliated with or endorsed by any game or hardware
maker.

- [Games](#games)
- [Install](#install)
- [First start](#first-start)
- [The board](#the-board)
- [Installing into a game](#installing-into-a-game)
- [Controllers](#controllers)
- [Your own games and DCS aircraft](#your-own-games-and-dcs-aircraft)
- [Backups](#backups)
- [Settings](#settings)
- [Your data and privacy](#your-data-and-privacy)
- [Help and bug reports](#help-and-bug-reports)
- [AI disclaimer](#ai-disclaimer)
- [Licence](#licence)

## Games

- **Elite Dangerous**
- **War Thunder**
- **X4: Foundations**
- **DCS World:** UH-60L, Su-25T, JAS 39 Gripen and F-14 ship with Tengwar. Any other aircraft you
  have installed can be added in a minute, from its own files: see
  [Your own games and DCS aircraft](#your-own-games-and-dcs-aircraft).

**A limitation: the shipped DCS aircraft.** Only aircraft the maintainer owns and has flown with
Tengwar ship with it, so the list grows slowly and many modules are missing. That doesn't stop you
using them: **Add a DCS aircraft** reads any module you have installed. If one you added works well,
[open an issue](../../issues) with its file so it can be checked and shipped for everyone.

## Install

1. Download `Tengwar-Setup-<version>-win-x64.exe` from the [newest release](../../releases/latest).
2. Run it. Windows may warn that the publisher is unknown, because the installer isn't signed yet:
   choose **More info**, then **Run anyway**. Tengwar installs for your Windows user only, without
   administrator rights.
3. Pick your options:
   - **DCS World aircraft importer**, ticked when DCS World is found on your PC. It's only needed to
     add DCS aircraft from their own files; untick it if you don't fly DCS.
   - **Desktop shortcut**, off by default.
4. Start Tengwar from the Start menu.

You need Windows 10 or 11 (64-bit). Tengwar's window needs the Microsoft Edge WebView2 Runtime, which
Windows 11 and an up-to-date Windows 10 already have (otherwise: `winget install Microsoft.EdgeWebView2Runtime`).

To check the download, compare it with `SHA256SUMS.txt` from the same release:
`Get-FileHash .\Tengwar-Setup-<version>-win-x64.exe` in PowerShell.

To update, run the newer installer over the old one. Your profile and settings stay.

## First start

The [first-time setup guide](guides/first-time-setup.md) walks through it step by step. In short:

1. **Your controllers.** Plug them in, then **Start fresh** with the ones you want (or import a profile
   file you exported before).
2. **Your games.** Tick the games you play. Games Tengwar finds on your PC are ticked already.
3. **Map controls.** Press each control when asked, so Tengwar knows which is which.
4. **Pick a game, set what each control does, fix anything red under Checks, and install.**

## The board

The main screen. Along the top: the game picker (DCS aircraft share one **DCS World** button, with a
list of your aircraft beside it), **Map controls**, **Device map** and **Export**.

- **The summary:** how many controls are identified, how many bindings you have, clashes, warnings, and
  important actions still on the keyboard only.
- **Checks:** everything worth a look before you install. Red means the file would be wrong (two jobs
  on one control in the same mode, say); amber is worth fixing; notes are for information.
- **The board itself:** every control on your devices, grouped as on the hardware, with what it does
  in this game. Press a control and it lights up. Filter by game mode (flight, landing, menus and so
  on) or search.
- **Click a control** to change what it does: search for an action and add it, or remove one. **Learn**
  in the same window identifies the control by pressing it.

Each game keeps its own layout. **Reset this game's layout** (under Profile, at the bottom) goes back to
the starting layout for that game.

## Installing into a game

Open **Export** at the top. Tengwar lists the steps for the game you're on.

- **Elite Dangerous:** **Install in the game** writes a custom binds file to Elite's bindings folder and
  switches all four control categories to it. Tengwar builds on your current binds file, so keyboard
  and on-foot bindings stay. Restart Elite, or open Controls once, to load it.
- **War Thunder:** **Save to exports** writes a `.blk` file. In War Thunder, open Controls, use
  **Import from file** (bottom left) and pick it.
- **X4: Foundations:** close X4 first (it rewrites its file when it quits). **Install in the game**
  rebuilds your `inputmap.xml`: joystick bindings are replaced, keyboard and mouse bindings stay.
- **DCS World:** under **Device map**, check each device's DCS file name (start DCS once with your
  controllers plugged in and Tengwar shows where to find it). Close DCS, then **Install in the game**
  writes one file per device into the aircraft's input folder.

Every file Tengwar replaces is backed up first (see [Backups](#backups)), and every file it builds is
also saved to `%LOCALAPPDATA%\Tengwar\exports`. **Copy** puts the file's text on the clipboard instead.

## Controllers

Any joystick, throttle, pedals, button box, gamepad or other HID game controller works. Tengwar ships
templates for a few devices; for any other, it builds one from what the controller reports: its axes
(X, Y, Z, Rx, Ry, Rz, Slider, Dial), its hats and its buttons, numbered as Windows and the games
number them. A built template works at once. **Map controls**, with "All of them", lets you name each
control and put it in a group on the board.

- **A controller plugged in later** shows under **Device map → Controllers on this PC**, with
  **Add to profile**.
- **Export template** on a device saves its template to share; **Import a device template** takes one.
- **Gamepads:** through the standard Windows controller interface, many gamepads (Xbox controllers
  among them) report both triggers as one axis. Tengwar can bind only that combined axis and says so
  on the control.
- **More than one hat:** every hat is written to the games, but only the first lights up live, so a
  second hat's directions can't be learned by pressing them.

## Your own games and DCS aircraft

Under **Settings → Your own games**:

- **Add a DCS aircraft** lists the aircraft installed in DCS and in your Saved Games mods folder. Pick
  one and Tengwar reads its own joystick file: every action, with the id DCS uses, grouped as DCS
  groups them. Tengwar only reads those files. A few commands use numbers that exist only inside DCS;
  Tengwar works out what it can and lists the rest under Checks, to bind in DCS itself. This needs the
  **DCS World aircraft importer** from the installer.
- **New game** adds a game that reads one of the file types Tengwar can write (a DCS aircraft, or a
  file like Elite's, War Thunder's or X4's). Type its actions in, or load them from a CSV file.

See the [guide to adding games](guides/adding-games.md). A game file with a problem is skipped and
listed under **Problems** in the same section; it never stops Tengwar from starting.

## Backups

Before Tengwar replaces a game file or your profile, it copies the old one to the backup folder and
checks the copy. If the backup can't be made (a drive that isn't plugged in, say), **nothing is
replaced**: Tengwar says so and offers to use the default folder instead.

- **Where:** `%LOCALAPPDATA%\Tengwar\backups` unless you pick another folder under
  **Settings → Backups**. A folder on another drive than your games is best.
- **Restore:** **Settings → Backups** lists every backup by game, with its date. **Restore** puts one
  back, after backing up what is there now.
- **Changing the folder:** Tengwar offers to copy your old backups to the new folder, checks every copy,
  and only then offers to remove the old ones.
- **Elite's own backups** (off by default): Elite leaves `.backup` files next to your bindings.
  **Collect the game's own backups** moves them into your backup folder.

## Settings

**Settings** (top right):

- **Game folders:** where each game keeps its files. Leave a field empty and Tengwar uses the game's
  own default; each folder shows the path in use and whether it's there.
- **Backups:** see above.
- **Your games:** which games show in the game picker. Turning one off hides it and keeps its layouts.
- **Your own games:** see above.
- **Program:** the local port Tengwar uses, and the short intro when it starts.

## Your data and privacy

Tengwar only reads your controllers. It never sends input to a game, and it only writes the game files
you ask it to install.

Tengwar never goes online: it has no account, no telemetry and no update check. Its window talks only
to Tengwar itself, on your own PC.

Everything it keeps stays on your PC, in `%LOCALAPPDATA%\Tengwar`:

| File or folder | What |
| --- | --- |
| `profile.json` | Your devices, what each control reads, your layouts per game |
| `settings.json` | Game folders, backup folder, your games |
| `exports\` | Every file Tengwar built |
| `backups\` | Files Tengwar replaced (unless you picked another folder) |
| `catalog\` | Games and device templates you added |

**Open data folder** (under Profile, on the board) opens it. To move to another PC, copy
`profile.json`, or import it on first start.

To uninstall: Windows Settings, Apps, **Tengwar**, Uninstall. Your data stays in
`%LOCALAPPDATA%\Tengwar`, so a reinstall keeps your layouts; delete that folder to remove it too.

## Help and bug reports

[Open an issue](../../issues) and say what you did, what you expected and what happened. Please
include:

- your Tengwar version (Windows Settings, Apps, Tengwar);
- the game, and for DCS the aircraft;
- your controllers, if it's about a device;
- the file Tengwar built, from `%LOCALAPPDATA%\Tengwar\exports`, if a binding is wrong in the game.

Your `profile.json` helps too, but it holds your device ids and layouts: only attach it if you're happy
to share those.

## AI disclaimer

AI tools have been used in making Tengwar: to plan its architecture, and to write code comments,
commit messages and documentation, including this guide. See the [disclaimer](DISCLAIMER.md).

## Licence

Tengwar is free to download and use, but not open source: see [LICENSE](LICENSE). Please share the
[releases page](../../releases) rather than the installer. Tengwar includes other people's work under
their own licences: see [THIRD-PARTY-NOTICES.md](THIRD-PARTY-NOTICES.md).
