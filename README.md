# Send to Other View for Notepad++

Send to Other View is a native Notepad++ plugin for copying or moving text from the active editor to the document open in the opposite view.

The current release is **1.8.0** and supports both 64-bit and 32-bit Notepad++ 8.0 or later.

## Download

- **64-bit Notepad++:** `dist/SendToOtherView-1.8.0-x64.zip`
- **32-bit Notepad++:** `dist/SendToOtherView-1.8.0-x86.zip`

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

Open two documents in Notepad++ and move one into the opposite view with **View > Move/Clone Current Document > Move to Other View**. The plugin commands then appear under **Plugins > Send to Other View** and in the editor context menu.

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

Copy and move operations are undoable. The plugin also warns when the opposite view has no document, a document is read-only, or a selection command has no selected text.

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

The timestamp option is enabled each time the plugin loads and affects only SMART Copy commands.

## Version history

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
