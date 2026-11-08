# Adding games and DCS aircraft

Tengwar ships with a few games. You can add more yourself, under **Settings → Your own games**. What
you add is kept in `%LOCALAPPDATA%\Tengwar\catalog\games\`, one file per game, and stays when you
update Tengwar.

- [A DCS aircraft](#a-dcs-aircraft)
- [A new game](#a-new-game)
- [Actions as CSV](#actions-as-csv)
- [When a game file has a problem](#when-a-game-file-has-a-problem)
- [Sharing what you added](#sharing-what-you-added)
- [Advanced: a game file by hand](#advanced-a-game-file-by-hand)

## A DCS aircraft

Any aircraft installed in DCS World can be added from its own files, in about a minute.

You need:

- the **DCS World aircraft importer**, an option in the Tengwar installer (ticked when DCS is on your
  PC). Missing it? Run the installer again and tick it.
- DCS World's install folder. Tengwar finds it by itself; if it doesn't, set it under
  **Settings → Game folders → DCS World install folder**.

Then:

1. **Settings → Your own games → Add a DCS aircraft.** Tengwar lists the aircraft installed in DCS and
   in `Saved Games\DCS\Mods`. Many aircraft? Type in **Find an aircraft**.
2. **Read** the one you want. Tengwar reads the aircraft's joystick file the way DCS does and shows what
   it found: how many actions, in how many groups (DCS's own categories).
3. **Save as a game.** Tengwar reloads with the aircraft in the game picker, under **DCS World**.

Good to know:

- **Tengwar only reads** the aircraft's files. It never changes anything in DCS's folders.
- **A few commands can't be read.** Some aircraft use commands that DCS numbers only inside the game,
  not in any file. Tengwar learns those numbers from the aircraft it already knows; any it still can't
  work out are listed when you read the aircraft. Bind those in DCS itself.
- **Reading an aircraft Tengwar ships** (the F-14, say) updates it from your installed version. Your
  layout for it is kept.
- **Aircraft with more than one cockpit** or variant show once per input profile; read the one you fly.

## A new game

**New game** is for a game that reads a file Tengwar can already write:

| The file the game reads | Example | Tengwar |
| --- | --- | --- |
| DCS World aircraft (`.diff.lua` per device) | an aircraft the importer can't read | installs it into DCS |
| Elite Dangerous style (`.binds`) | | installs it into Elite's bindings folder |
| X4: Foundations style (`inputmap.xml`) | | installs it into the X4 profile |
| War Thunder style (`.blk`) | | saves it to exports; the game imports it |

A game with a file of its own needs Tengwar to learn that file first: [open an issue](../../../issues)
asking for it, with an example of the file the game writes.

Fill in:

- **Name** and **Short name** (shown in the game picker).
- **The file the game reads**, and its file name if asked.
- **Modes**, one per line as `id: name`, for example `flight: Flight` and `menu: Menus`. Two jobs on one
  control clash only when they're in the same mode.
- **Actions**, typed in or loaded from a CSV file: see below.

**Save.** Tengwar checks the game first and tells you what to fix, if anything. A new game is ticked under
**Your games** straight away.

To change a game later: **Edit** next to it in **Your own games**.

## Actions as CSV

One action per line: `tag,label,kind,mode,hold`. A first line naming the columns is skipped.

```
tag,label,kind,mode,hold
FIRE,Fire,btn,flight
ROLL_AXIS,Roll,axis,flight
MAP,Galaxy map,btn,menu,hold
```

| Column | What |
| --- | --- |
| `tag` | The game's own id for the action, exactly as the game's file writes it. |
| `label` | The name you see in Tengwar. |
| `kind` | `btn` for a button, `axis` for an axis. A control only takes actions of its own kind. |
| `mode` | A mode id or name. A mode that isn't listed yet is added. |
| `hold` | Optional: `hold` when the action works while the button is held. |

Get the tags from the game's own files (a default bindings file, say), not by guessing: a wrong tag
means the game ignores that binding. Spreadsheets save CSV with **Save as → CSV**.

## When a game file has a problem

Tengwar checks every game file you added each time it starts. A file with a problem is skipped and listed
under **Settings → Your own games → Problems**, with what's wrong. It never stops Tengwar from starting.
Fix the file (or remove it from `%LOCALAPPDATA%\Tengwar\catalog\games\`) and restart Tengwar.

## Sharing what you added

Added an aircraft or a game that works well? [Open an issue](../../../issues) and attach its file from
`%LOCALAPPDATA%\Tengwar\catalog\games\`. It can then be checked and shipped with Tengwar for everyone.
The file holds only the game's actions, never your layout or your devices.

## Advanced: a game file by hand

A game is one JSON file in `%LOCALAPPDATA%\Tengwar\catalog\games\`, read when Tengwar starts. **New
game** writes the same file; by hand you can set a few more things:

```json
{
  "id": "example",
  "name": "Example Game",
  "short": "Example",
  "format": "wt-blk",
  "blurb": "One line about what the layout covers.",
  "ctx": { "ship": "Flight", "menu": "Menus & maps" },
  "ctxOrder": ["ship", "menu"],
  "actions": [
    { "tag": "BOOST", "kind": "btn", "hold": false, "ctx": "ship", "label": "Boost" },
    { "tag": "YAW_AXIS", "kind": "axis", "hold": false, "ctx": "ship", "label": "Yaw" }
  ],
  "essential": ["BOOST"],
  "pairs": [],
  "maxSlots": 2,
  "install": { "kind": "export-only", "file": "example.blk" }
}
```

| Field | Meaning |
| --- | --- |
| `id` | Lower-case letters, digits and dashes. A file with the same `id` as a shipped game replaces it. |
| `format` | `elite-binds`, `wt-blk`, `x4-inputmap` or `dcs-diff-lua`. |
| `ctx`, `ctxOrder` | The modes, and their order on the board. |
| `essential` | Actions Checks warns about when no controller has them. |
| `pairs` | Pairs of actions that may share a control even in the same mode, because they never happen together. |
| `maxSlots` | How many controls one button action may sit on (Elite has two). |
| `install.kind` | `elite-bindings`, `x4-inputmap`, `dcs-input`, or `export-only` (you import the file in the game). |

Tips for a good layout, from games mapped so far:

- Reuse muscle memory: the trigger fires, and the same hat does the same kind of job in every game.
- Next and previous of the same thing go on the same side of a grip.
- A latching switch is a held button: good for modes and arming, bad for one-shot toggles.
- Keep buttons you use for other things (head tracking, say) free.
