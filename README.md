# Send to Other View for Notepad++

Send to Other View is a native Notepad++ plugin for copying or moving text from the active editor to a configured destination file in the opposite view.

The current release is **1.9.0** and supports both 64-bit and 32-bit Notepad++ 8.0 or later.

## Download

- **64-bit Notepad++:** [Download SendToOtherView-1.9.0-x64.zip](https://github.com/StephenWalker999/SendToOtherViewPUBLIC/releases/download/v1.9.0/SendToOtherView-1.9.0-x64.zip)
- **32-bit Notepad++:** [Download SendToOtherView-1.9.0-x86.zip](https://github.com/StephenWalker999/SendToOtherViewPUBLIC/releases/download/v1.9.0/SendToOtherView-1.9.0-x86.zip)

Choose the package that matches your Notepad++ installation. In Notepad++, select **? > Debug Info...** if you are unsure which architecture you use.

## Installation

1. Close Notepad++ completely.
2. Extract the matching release ZIP.
3. Run `install.ps1` from the extracted folder.
4. Restart Notepad++.

The installer places `SendToOtherView.dll` in the correct plugin folder and adds the transfer commands to the editor context menu. It can be run again when upgrading.

For a manual installation, create a `SendToOtherView` folder inside the Notepad++ `plugins` folder and copy `SendToOtherView.dll` into it. The final path should be:

```text
Notepad++\plugins\SendToOtherView\SendToOtherView.dll
```

## Using the plugin

The plugin commands appear under **Plugins > Send to Other View** and in the editor context menu. By default, filenames such as `#40227_Example.log` resolve to `#40227_Notes.txt` in the same folder. When a source filename does not match the configured pattern, the plugin uses the document currently selected in the opposite view.

Available transfer commands:

- **Copy selection** copies the selected text exactly.
- **Copy trimmed selection** removes leading and trailing spaces from each selected line before copying. Tabs are preserved.
- **Copy SMART selection** cleans structured text and keeps the fields shared by every selected line.
- **Copy SMART line(s)** applies SMART processing to every complete line touched by the selection, or to the current line when there is no selection.
- **Copy selected line(s)** copies complete selected lines, or the current line when there is no selection.
- **Move selected line(s)** copies complete lines to the opposite view and removes them from the source.

Choose where transferred text is placed with one of these mutually exclusive options:

- **Append to end of file** — the default.
- **Insert at start of file**.
- **Insert at current cursor location** in the opposite view.

The insertion position and SMART timestamp option persist between Notepad++ sessions. Select **Settings ...** to open the plugin configuration file in the current Notepad++ instance.

Copy and move operations are undoable. The plugin also warns when a required destination is unavailable, a document is read-only, or a selection command has no selected text.

## Scratchpad destination routing

The plugin creates `SendToOtherView.ini` in Notepad++'s per-user plugin configuration directory, normally `%APPDATA%\Notepad++\plugins\Config`. Its default scratchpad configuration is:

```ini
[README]
IMPORTANT=If you change this file manually, restart Notepad++ for the changes to take effect.

[Scratchpad]
SourcePattern=(?<fullprefix>(?:#)(?<identity>[^_]+)(?:_))(?<name>.*)(?<suffix>\.log)
DestinationPattern=#(?<identity>)_Notes.txt
DestinationTemplate=Ticket No:#(?<identity>)_Notes.txt\n(?<fullprefix>)\n\nName: (?<name>)\nSuffix: (?<suffix>)\n\n------
CreateMissingFiles=false

[Location]
InsertPosition=End

[SMART]
RemoveLeadingTimestamp=true
```

`SourcePattern` uses named capture groups. Those captures can be inserted into `DestinationPattern` to select the destination filename and into `DestinationTemplate` to populate a newly created file. The template recognizes `\n`, `\r`, `\t`, and `\\` escape sequences.

For example, the source file `#40227_Example.log` resolves to `#40227_Notes.txt`. If that destination is created, its initial contents are:

```text
Ticket No:#40227_Notes.txt
#40227_

Name: Example
Suffix: .log

------
```

When `CreateMissingFiles=false`, the plugin asks before creating a missing destination; accepting the prompt also enables automatic creation for future transfers. The template is used only for a new destination and never overwrites an existing file. `InsertPosition` accepts `End`, `Start`, or `Cursor`; the Boolean options accept `true`/`false`, `yes`/`no`, `on`/`off`, or `1`/`0`. Restart Notepad++ after manually editing the INI.

## SMART Copy

SMART Copy is useful for log lines and delimiter-separated data. For each selected line it can:

1. Remove a four-digit timestamp followed by one space when **SMART: Remove leading timestamp** is enabled.
2. Remove an initial alphanumeric label such as `INFO: ` or `A12: `.
3. Recognize commas and ` : ` as separators while ignoring separators inside quoted fields.
4. Keep the number of leading fields present in the shortest selected row, discarding surplus trailing fields.

For example:

```text
1234 INFO: Apple,"London, UK",Red,Large
1235 DATA: Banana,"Paris, France",Yellow
1236 ITEM: Cherry,"Rome, Italy",Red,Small,Fresh
```

becomes:

```text
Apple,"London, UK",Red
Banana,"Paris, France",Yellow
Cherry,"Rome, Italy",Red
```

The timestamp option is enabled by default, persists between plugin sessions, and affects only SMART Copy commands.

## Version history

### 1.9.0

- Added configurable source-pattern matching and destination filename templates using named captures.
- Added optional creation of missing destination files and templated initial file contents.
- Added silent fallback to the currently selected opposite-view document when a source filename does not match.
- Persisted the insertion position and SMART timestamp-removal option between sessions.
- Added **Settings ...** to open `SendToOtherView.ini` in the current Notepad++ instance.
- Added validation and user feedback for invalid patterns, templates, filenames, and inaccessible destinations.

### 1.8.0

- Added ` : ` as a SMART Copy field separator alongside commas.
- Preserved original separator text and continued ignoring separators inside quoted fields.
- Added a 32-bit release for 32-bit Notepad++.

### 1.7.0

- Added insertion at the end, start, or destination cursor.
- Applied the selected insertion position to every copy and move command.
- Simplified menu labels and organization.

### 1.6.0

- Added **Copy SMART line(s)** for processing complete selected lines or the current line.

### 1.5.1

- Expanded the About dialog into an in-application command guide.
- Clarified SMART processing and timestamp behavior.

### 1.5.0

- Restricted SMART label removal to ASCII letters and digits followed by a colon and exactly one space.

### 1.4.0

- Added optional removal of a four-digit leading timestamp.
- Added the checked **SMART: Remove leading timestamp** menu option.

### 1.3.0

- Introduced SMART selection copying with CSV-aware quoted-field handling.
- Added shared-field truncation based on the shortest selected row.

### 1.2.0

- Added per-line trimmed selection copying.
- Restored the **Send to Other View** editor context submenu.

### 1.1.0

- Added exact selection copying, including multiple and rectangular selections.
- Added an About command and improved installation and upgrade behavior.

### 1.0.0

- Initial 64-bit release.
- Added copying and moving of current or selected lines to the opposite view.
- Added destination line-ending handling, undo support, and read-only validation.

## License

See [LICENSE](LICENSE).
