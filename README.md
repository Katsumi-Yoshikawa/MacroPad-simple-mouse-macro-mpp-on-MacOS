# MacroPad | simple Mouse Macro App on MacOS

[简体中文](README.zh-CN.md)

## Overview

MacroPad is a native macOS utility for recording, editing, saving, triggering,
and replaying keyboard and mouse macros. It is built with SwiftUI and AppKit and
runs entirely on the local Mac. 

> I've tried to press and hold a hotkey to continuously activate SBA, but it was challenging for me while moving my melee characters around during a combat. I've also tried Mouse Macro softwares, incl. Razer Synapse and Logitech G-Hub, only compatible with their mice on Windows. With the sfotwares I can use toggle loop to start/stop macro (automatically press keys for SBA while not hold it). They are good but none of them work properly on MacOS (esp. MacOS 12 Monterey which I'm still working with). In addition, I've tried several other Apps, incl. Keyboard Masstro, BetterTouchTool, but they are too complicated only for WOW SBA. 
> Watch the demo how MacroPad works for Single-Button Assistant in World of Warcraft: https://youtu.be/bSpDPEKcC54

## Features

- Record mouse button presses/releases, scrolling, keyboard presses/releases,
  and modifier changes.
- Edit event delays, click coordinates, mouse buttons, keys, modifiers, and
  scroll deltas.
- Enable, disable, or delete individual events.
- Save macros as versioned JSON files and automatically reopen the most recent
  macro file on the next launch.
- Control playback speed and loop count.
- Assign a mouse button to one of three trigger modes: single shot, hold to
  loop, or click to toggle looping.
- Keep recording, playback, and triggers available from the macOS menu bar when
  the main window is hidden.

## Requirements

- macOS 12 Monterey or later (not tested on Apple silicon yet)
- Xcode Command Line Tools with Swift 5.7 or later (https://developer.apple.com/support/xcode)

MacroPad has no third-party package dependencies.

## Build from Source

From the repository root:

```bash
swift test
./script/build_and_run.sh
```

The script builds a local development app at `dist/MacroPad.app` and opens it.
It is not intended to produce a signed distribution build.

To build only the Swift executable:

```bash
swift build
```

## Permissions

MacroPad follows macOS privacy controls and does not bypass permission checks.

- **Input Monitoring** is required to record input and listen for mouse-button
  triggers.
- **Accessibility** is required to replay keyboard and mouse events.

Grant these permissions in **System Settings > Privacy & Security** when
prompted. If macOS does not apply a new permission immediately, quit and reopen
MacroPad.

## Usage

1. Grant the required macOS permissions.
2. Use **Record** to capture input. Mouse movement and drag events are ignored.
3. Use **Stop** or the stop-recording shortcut to end recording.
4. Select an event to edit its timing and supported parameters.
5. Set macro speed, loop count, and an optional mouse-button trigger in the
   inspector.
6. Use **Play** to run the selected macro.
7. Use **Save** and **Load** to manage macro JSON files.
8. Use the trash button below the macro list to remove the selected macro from
   the list. Its JSON file remains on disk.

Closing the main window hides it without quitting MacroPad. Use the MacroPad
menu bar item to show the window again, control recording/playback, inspect
permission status, or quit the app.

## Global Shortcuts

| Shortcut | Action |
| --- | --- |
| `Option-Command-R` | Start or stop recording |
| `Option-Command-P` | Start or stop playback |
| `Option-Command-S` | Stop recording and remove the trailing stop-shortcut events from the recording |

The shortcuts are currently fixed. Registration can fail when another app is
already using the same key combination.

## Macro Files and Privacy

Macro files are human-readable JSON files stored at locations selected by the
user. MacroPad remembers the most recently opened or saved file using local
macOS bookmark data.

MacroPad has no network component and does not upload recorded events or macro
files. Recorded macros may contain sensitive keystrokes or click locations, so
review JSON files before sharing or committing them to a repository.

## Known Limitations

- macOS only; no prebuilt or notarized app is included in the initial release.
- Continuous mouse movement and mouse dragging are not recorded.
- Only one macro can play at a time.
- Global shortcuts are not configurable.
- There is no image recognition, conditional scripting, scheduling, or
  application/window targeting.
- Some applications may reject generated input. Automation may also be
  restricted by an application's or game's terms of service; use MacroPad only
  where automation is permitted.

## Testing

Run the complete test suite from the repository root:

```bash
swift test
```

## License

MacroPad is available under the [MIT License](LICENSE).
