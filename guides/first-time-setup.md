# First-time setup

From installing Tengwar to your first layout in a game, in about fifteen minutes. You'll need your
controllers plugged in and, for the last step, the game closed.

- [1. Install](#1-install)
- [2. Your controllers](#2-your-controllers)
- [3. Your games](#3-your-games)
- [4. Map your controls](#4-map-your-controls)
- [5. Make your layout](#5-make-your-layout)
- [6. Install it into the game](#6-install-it-into-the-game)
- [7. Check it in the game](#7-check-it-in-the-game)
- [Before you start: a backup folder](#before-you-start-a-backup-folder)
- [If something goes wrong](#if-something-goes-wrong)

## 1. Install

1. Download `Tengwar-Setup-<version>-win-x64.exe` from the [newest release](../../../releases/latest).
2. Run it. If Windows says the publisher is unknown, choose **More info**, then **Run anyway** (the
   installer isn't signed yet).
3. If you fly DCS World, keep **DCS World aircraft importer** ticked. It's ticked already when DCS is
   on your PC.
4. Finish, and let the installer start Tengwar.

## 2. Your controllers

Plug in every controller you want to use **before** this step: stick, throttle, pedals, button boxes,
gamepad.

Tengwar asks for a profile, which holds your controllers and your layouts:

- **Start fresh** with the controllers it lists. Tick the ones you want to use (it ticks the connected
  ones). A controller Tengwar has no template for gets one built from what it reports; you'll name its
  controls in step 4. Missing one? Plug it in and press **Look again**.
- **Import a profile file** if you exported one from Tengwar before, on another PC say.

## 3. Your games

Tick the games you play. Games Tengwar finds on your PC are ticked already, from the folders the games
make themselves:

- **Elite Dangerous:** its Options folder.
- **DCS World:** an aircraft is ticked once DCS has made its input folder for it, which happens the first
  time you open its controls in DCS. All aircraft sit under **DCS World**: tick that to take them all.
- **X4: Foundations:** its folder in Documents.
- **War Thunder** is never found by itself: tick it if you play it.

**Continue**, and you're on the board. You can change the games any time under **Settings → Your games**.

## 4. Map your controls

Tengwar needs to know which physical control is which. Press **Map controls** at the top.

1. Choose **Only the ones not identified yet** (or **All of them, from the top** for a controller you
   want to name yourself), then **Start**.
2. Tengwar names a control. **Press it**, or for an axis **move it from one end to the other**. Tengwar
   shows what it saw and moves on.
3. On a built template you can **name** each control and put it in a **group** on the board as you go.
4. Don't have that control, or don't want it? **Skip**. Pressed the wrong one? **Back**.

You can stop at any time and come back later; what you did is saved. To do just one control: click it on
the board, then **Learn** and press it.

## 5. Make your layout

1. **Pick a game** at the top. For DCS, press **DCS World** and pick the aircraft from the list beside it.
2. **Click a control** on the board. Search for an action (say "landing gear") and add it. A control can
   do one thing per game mode: flight and landing, say.
3. Look at **Checks**. Fix anything red first: it would make a wrong file. Amber is worth a look; notes
   tell you which important actions are still on the keyboard only.

Your layout saves as you go, separately for each game. Pressing any control lights it up on the board,
which is the quickest way to find it.

## 6. Install it into the game

**Close the game first.** Then press **Export** at the top, and follow the steps it lists for that game:

| Game | What to do |
| --- | --- |
| Elite Dangerous | **Install in the game**. |
| X4: Foundations | **Install in the game**. |
| War Thunder | **Save to exports**, then in War Thunder: Controls, **Import from file** (bottom left), and pick the file. |
| DCS World | Under **Device map**, fill in each device's **DCS file name** if Checks asks for it (see below). Then **Install in the game**. |

Before anything in the game's folder is replaced, Tengwar backs the old file up and checks the copy.

**DCS file names.** DCS names each controller's file after the controller's name and its Windows id,
like `Throttle Name {12345678-ABCD-...}`. Start DCS once with your controllers plugged in, then look in
`Saved Games\DCS\Logs\dcs.log` for your device's name with its `{...}` id after it, and copy that line's
name and id into the field under **Device map**.

## 7. Check it in the game

- **Elite Dangerous:** restart the game, or open Options, Controls once. The preset is **Custom**.
- **X4: Foundations:** start the game and look at Controls.
- **War Thunder:** after the import, the controls are in place.
- **DCS World:** open Controls, pick the aircraft, and use **Axis Tune** on the throttle: pushing it
  forward should add power. If it runs backwards, go back to Tengwar, open the throttle control, change
  **Invert**, and install again.

Something not right? Change it in Tengwar and install again; each install makes a fresh backup.

## Before you start: a backup folder

Optional, but worth a minute: under **Settings → Backups**, pick a folder on **another drive** than your
games. Then a broken drive can't take your game files and their backups with it.

## If something goes wrong

- **Undo an install:** **Settings → Backups**, find the game and the time, and **Restore**.
- **Tengwar shows no live input** ("Connecting" or "Reconnecting" at the top): close Tengwar and start
  it again from the Start menu.
- **A controller isn't listed:** plug it in, then **Look again** (on first start) or **Device map →
  Look again**.
- **A game folder isn't found:** set it under **Settings → Game folders**.
- Still stuck? [Open an issue](../../../issues).
