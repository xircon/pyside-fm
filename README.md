# pyside-fm

`pyside-fm` is a dual-pane file manager written in Python with PySide6.

This project is developed with AI assistance. Code, UI behavior, documentation, and iteration notes have been created and refined through human direction with AI-generated implementation support.

## Screenshot

![pyside-fm screenshot](2026-06-27_20-52.png)

## Features

- Dual-pane file browsing with independent paths and view modes.
- Icon, list, and details views.
- Breadcrumb navigation and compact `~/...` path display.
- Sidebar with favorites, places, recent folders, tree view, and Trash shortcut.
- Copy, move, duplicate, rename, archive, extract, trash, delete, and undo support.
- Drag and drop copy/move between panes.
- Text, image, and PDF previews.
- Full-pane preview in the opposite pane, with Escape to close.
- PDF preview page navigation.
- Configurable icon layout density: Compact, Normal, Spacious.
- Per-pane icon zoom persistence.
- Theme support: Light, Dark, Very Dark.
- Custom user toolbar buttons.
- Open With menu using cached desktop entries and cached application icons.

## Requirements

- Python 3
- PySide6
- PySide6 QtPdf support

Run directly:

```bash
./fm
```

Keep it attached to the launching terminal:

```bash
./fm --no-detach
```

Open with optional pane paths and view modes:

```bash
./fm ~/Downloads icon ~/Documents details
```

Valid view modes:

```text
icon
list
details
```

## Main Window

The app has two file panes:

- Left pane
- Right pane

Each pane has:

- Navigation buttons
- Path field
- Search field
- Icon zoom buttons
- View mode selector
- Breadcrumb buttons
- File view
- Status line
- Optional preview area

The active pane is highlighted. Most commands operate on the active pane.

## Toolbar

The top toolbar contains:

- New Folder: create a folder in the active pane.
- New File: create a file in the active pane.
- Rename: rename the selected item.
- Copy Across: copy selected or tagged items to the other pane.
- Move Across: move selected or tagged items to the other pane.
- Trash: move selected or tagged items to Trash.
- Empty Trash: permanently remove contents of `~/.local/share/Trash/files` and clear matching trash info.
- Terminal Here: open the configured terminal in the active pane folder.
- Terminal Home: open the configured terminal in `~`.
- Properties: show properties for the selected item or current folder.
- Hidden: toggle hidden files.
- Preview: toggle automatic preview panes.
- Swap Panes: swap left and right pane paths and view modes.
- Side Panel: show or hide the side panel.
- Settings: open app settings.

Custom user buttons can be added in Settings. Each user button can have:

- Label
- Symbol or icon
- Command

Icon values can be:

```text
icon:theme-icon-name
/path/to/icon.png
plain text glyph
```

User commands support placeholders:

```text
{path}      active pane path
{left}      left pane path
{right}     right pane path
{selected}  selected or tagged paths
```

## Sidebar

The sidebar has two tabs:

- Shortcuts
- Tree

Shortcut sections include:

- Favorites
- Places
- Recent

Default places include:

- Home
- Desktop
- Downloads
- Documents
- Pictures
- Music
- Videos
- tmp
- scripts
- Trash
- Root

Favorite/recent context menu actions:

- Rename Favorite
- Move Up
- Move Down
- Remove Favorite
- Remove Recent
- Clear Recent

Tree context menu actions:

- Open
- Add to Favorites
- Terminal Here
- Calculate Size

## Selection

Normal selection uses the current file view selection.

Details view also supports tagging:

- Press Space to tag or untag the current row.
- Tagged files take priority over ordinary selection for copy/move/trash operations.
- Press Escape to clear selection if no manual preview is open.

In icon view, empty space between icon hit areas can be used to start rubber-band selection.

## Context Menu

Right-click in a file pane opens the file context menu.

Actions:

- Open: open folder in the current pane, or open file with the desktop default handler.
- Open With: lazily loads matching desktop applications for the selected file type.
- Other Command: enter a command manually.
- New Folder: create a folder in the current pane.
- New File: create a file in the current pane.
- Rename: rename the selected item.
- Duplicate: duplicate selected items.
- Create Archive: create an archive from selected items.
- Extract Here: extract selected archive into the current folder.
- Extract To: extract selected archive into a new chosen folder.
- Add to Favorites: add selected path to the sidebar favorites.
- Open in Other Pane: open selected folder in the opposite pane.
- Preview in Other Pane: show selected text, image, or PDF file in the opposite pane.
- Copy to Other Pane: copy selected/tagged items to the opposite pane.
- Move to Other Pane: move selected/tagged items to the opposite pane.
- Move to Trash: move selected/tagged items to Trash.
- Delete Permanently: permanently delete selected/tagged items.
- Terminal Here: open a terminal in the current folder.
- Calculate Size: recursively calculate size, file count, and folder count.
- Properties: show item properties.

## Preview

Automatic preview can be toggled with the toolbar Preview action.

Supported preview types:

- Text files
- Image files
- PDF files

Manual peer preview:

1. Right-click a supported file.
2. Choose `Preview in Other Pane`.
3. The opposite pane becomes a full-pane preview.
4. Press Escape to close and return to the normal file view.

PDF preview:

- Shows rendered PDF pages.
- Uses a light preview background for readability.
- Previous and Next buttons move between pages.
- Page label shows the current page and total page count.

PDF keyboard controls while preview is open:

- Next page: PageDown, Right, Down
- Previous page: PageUp, Left, Up
- Close preview: Escape

## Keyboard Shortcuts

Navigation:

| Action | Shortcut |
| --- | --- |
| Open selected | Enter / Ctrl+O |
| Go back | Backspace / Alt+Left |
| Go forward | Alt+Right |
| Go up | Alt+Up |
| Focus path bar | Ctrl+L |
| Focus pane search | Ctrl+F |
| Refresh | Ctrl+R |

File operations:

| Action | Shortcut |
| --- | --- |
| Copy selected or tagged files | Ctrl+C |
| Paste copied files into active pane | Ctrl+V |
| Move selected or tagged to other pane | Ctrl+M |
| Undo last operation | Ctrl+Z |
| Move to trash | Delete |
| Delete permanently | Shift+Delete |
| Rename | F2 |
| New folder | F7 |
| New file | Ctrl+N |
| Open terminal here | F4 |
| Properties | Alt+Return |

Panes and selection:

| Action | Shortcut |
| --- | --- |
| Copy to other pane | F5 |
| Move to other pane | F6 / Ctrl+M |
| Tag or untag row in detailed view | Space |
| Swap panes | Toolbar button |
| Drag copy | Drag and drop |
| Drag move | Shift+drag and drop |

Display and app:

| Action | Shortcut |
| --- | --- |
| Toggle hidden files | Ctrl+H |
| Zoom icons larger | Ctrl++ / Ctrl+= |
| Zoom icons smaller | Ctrl+- |
| Toggle side panel | Ctrl+B / F9 |
| Settings | Ctrl+, |
| Help | F1 |
| Quit | Ctrl+Q |
| Close help or manual preview | Escape |

## Settings

Settings include:

- Theme
- Icon layout
- Terminal command
- Terminal arguments
- Four custom user toolbar buttons

Default terminal:

```text
kitty
```

Default terminal arguments:

```text
--app-id=org.ai.floater
```

Icon layout presets:

- Compact
- Normal
- Spacious

## Trash

Trash uses the freedesktop user trash location:

```text
~/.local/share/Trash/files
~/.local/share/Trash/info
```

Move to Trash records undo information.

Empty Trash permanently removes files from Trash and clears trash metadata.

## Archives

Supported archive extensions:

```text
.zip
.tar
.tar.gz
.tgz
.tar.bz2
.tbz2
.tar.xz
.txz
```

Archive actions:

- Create Archive
- Extract Here
- Extract To

## Development Notes

The app version is stored in:

```python
APP_VERSION
```

Project convention:

- Update `APP_VERSION` for app source changes.
- Back up the previous build in this project directory before source edits:

```text
fm<version>.zip
```

Example:

```text
fm0.72.zip
```

Backup zip files are ignored by Git.

## Git Workflow

Check status:

```bash
git status
```

Stage changes:

```bash
git add fm README.md fm.desktop .gitignore
```

Commit:

```bash
git commit -m "Describe the change"
```

Push:

```bash
git push
```
