# claude-multi-profile

Two independent Claude Desktop windows (Windows, MSIX install) with different accounts, running at the same time.

Claude Desktop is an Electron app, so a second instance can be started with a separate data directory via `--user-data-dir`.

## Files

| File | What it does |
|---|---|
| `launch-profile1.cmd` | Starts Claude with the default profile (`%APPDATA%\Claude`), window title `Profile1` |
| `launch-profile2.cmd` | Starts Claude with a separate profile (`%APPDATA%\Claude-Profile2`), window title `Profile2` |

Each launcher:
1. Finds the current `claude.exe` path via `Get-AppxPackage -Name Claude` (the path contains the package version, so updates don't break it).
2. Starts the app (the second profile with `--user-data-dir`).
3. In a hidden PowerShell window, sets the window title every second via Win32 `SetWindowTextW` while the app is running.

All code is embedded in the `.cmd` files (no `.ps1`), to avoid PowerShell execution-policy problems.

## Install

1. Copy the `.cmd` files to `%USERPROFILE%\ClaudeWork\`.
2. Create desktop shortcuts to them (icon: `claude.exe` from the package).
3. Run the second shortcut and sign in to the desired account; the login is stored in its own directory.

To add another account: copy `launch-profile2.cmd` and replace `Claude-Profile2` and the title.
