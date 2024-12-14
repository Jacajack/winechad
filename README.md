# winechad

This is a silly little tool for WINE prefix management. The aim here is to create a simpler, more robust and GUI-less alternative to PlayOnLinux.

Features:
 - Multiple prefix and app management.
 - Simple per-prefix TOML configuration. This makes backups and moving stuff between machines much easier.
 - Supports self-contained prefixes (including fake home, WINE binaries and configuration)
 - Integration with `firejail`
 - Integration with `winetricks`

At some point this tool will need a major refactor, cause the internals have gotten quite messy. Especially stuff related to converting paths etc.
The code is also only tested through "normal" use, so use at own risk.

# Configuration 

The main config file should be located at `~/.config/winechad/config,toml`:

```toml
[general]

# Where you keep your WINE installations
wine_dir = "/path/to/your/wines"
 
# List of directories where the prefixes will be searched for
prefix_dirs = ["/my/prefix/collection"] 
```

This configuration instructs Winechad to search for WINE prefixes in `/my/prefix/collection`. A directory is considered a Winechad prefix if it contains a `winechad.toml`.
An example prefix configuration might look like this:

```toml
# /my/prefix/collection/my_app/winechad.toml
[prefix]

# Name of the prefix
name = "my_app"

# Prefix description
description = "I keep my_app here."

# WINE version string
wine = "6.17"

# Is this a 64-bit prefix? Winechad will try to determine that automatically.
# wine64 = 

# Default app to be ran in this prefix.
# Useful when you have one app per prefix.
default_app = "my_app"

# Whether firejail should be used. ON by default
# firejail_enabled = true

# Whether firejail should use a jail home directory. OFF by default.
# firejail_home = true

# What firejail profile to use. If not specified, --noprofile is used.
# firejail_profile =

# This section describes all apps contained in this prefix
[[apps]]

# Name of the application
name = "app"

# Path to the executable within the prefix
path = "C:\\Program Files (x86)\\MyApp\\my_app.exe"

# Description of the app (optional)
# description =

# Additional args to be passed to the EXE file
# args = []

# Additional environment vars to be set for the application
# env = {}
```

# Usage 

To see help, try `winechad --help`.

The supported sub-commands are:
```
run (r)             Run WINE application
apps                List WINE apps
prefixes            List WINE prefixes
sandbox             Configure WINE prefix for isolated operation
configure           Configure WINE prefix
reboot              Reboot WINE prefix
control             Open Control Panel
taskmgr             Open Task Manager
regedit             Open Registry Editor
tricks              Run winetricks
cmd                 Open CMD.EXE
```
