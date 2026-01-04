# Gutipoka CMD

A concise, reproducible setup to customize Windows Command Prompt / PowerShell using Fastfetch, UTF-8 support, and a custom terminal appearance.

This project treats terminal configuration as code—structured, repeatable, and easy to move to a new machine.

## Overview

This repository contains:
- A customized Command Prompt / PowerShell appearance
- Fastfetch configuration with custom ASCII art
- Terminal settings for fonts, colors, and layout
- A PowerShell profile that initializes the environment correctly

The goal is simple:
open CMD or PowerShell → instantly get a clean, themed system overview.

Follow the steps below to reproduce the setup.

## Screenshot

Current state of my command prompt:

![Gutipoka CMD screenshot](Gutipoka%20CMD.png)


## Repository Structure
```powershell
.
├── Command Prompt/
│   └── settings.json			# Windows Terminal / CMD appearance config
│
├── PowerShell/
│   └── profile.ps1			# PowerShell startup profile
│
├── fastfetch/
│   ├── ascii.txt				# Custom ASCII art
│   └── config.jsonc			# Fastfetch configuration
├── Gutipoka CMD.png			# Screenshot (example output)
├── JetBrains Mono.png     	# Font reference
│
├── LICENSE
└── README.md

```
## Prerequisites
- Windows 10 or Windows 11
- Windows Terminal (recommended, but CMD works too)
- PowerShell 5.1+ or PowerShell 7+
- Internet connection (for installing Fastfetch)

## Steps
**1. Install JetBrains Mono Font**

- Download the zip file [JetBrainsMono-2.304](JetBrainsMono-2.304)
- Extract everything
- Go to the fonts → ttf folder
- Select all → right click → install (everything will be installed)
- Open a new window in VScode → Settings
- Search font
- Go to font family → Put "JetBrains Mono" at the front (like in the give picture)

![JetBrains Mono screenshot](JetBrains%20Mono.png)

**2. Install Fastfetch**

*Using winget (recommended):*

```powershell
winget install fastfetch
```

If winget fails, install Fastfetch manually from [fastfetch official releases](https://github.com/fastfetch-cli/fastfetch) and ensure fastfetch is added to your PATH.

*Verify installation:*

```powershell

fastfetch
```

**3. Set up Fastfetch config directory**

Fastfetch looks for its config inside a .config directory in your user profile.

*Run the following in PowerShell:*

```powershell
New-Item -ItemType Directory -Path "$env:USERPROFILE\.config" -Force
attrib +h "$env:USERPROFILE\.config"

New-Item -ItemType Directory -Path "$env:USERPROFILE\.config\fastfetch" -Force
```

*Now copy the files from this repo (adjust the path):*

```powershell
Copy-Item -Path .\fastfetch\* `
  -Destination "$env:USERPROFILE\.config\fastfetch" `
  -Recurse -Force
```

*Alternatively, copy them manually into:*

```powershell
%USERPROFILE%\.config\fastfetch
```
**4. Configure Windows Terminal / Command Prompt**

- Open Windows Terminal → Settings → Open JSON file.
- Paste or merge the contents of: [Comand Prompt/settings.json](Comand%20Prompt/settings.json)
	- *Highly recommend going through them and only adding parts that are necessary*

1. Paste the Command Prompt settings

- Open Windows Terminal or Command Prompt settings and paste the JSON from:
  - [Comand Prompt/settings.json](Comand%20Prompt/settings.json)



3. Create or open your PowerShell profile

- Check your profile path in PowerShell:

```powershell
$PROFILE
```

- If the profile file does not exist, create it:

```powershell
New-Item -Path $profile.CurrentUserAllHosts -Type File -Force
```

- Edit the profile to run `fastfetch` on startup (optional):

```powershell
notepad $PROFILE
# or
code $PROFILE
```

Add a line like this to show Fastfetch at shell start:

```powershell
fastfetch
```

4. Create the `.config` folder and copy Fastfetch files

- Create a `.config` directory in your user profile and mark it hidden, then add a `fastfetch` folder:

```powershell
New-Item -ItemType Directory -Path "$env:USERPROFILE\.config" -Force
attrib +h "$env:USERPROFILE\.config"
New-Item -ItemType Directory -Path "$env:USERPROFILE\.config\fastfetch" -Force
```

- Copy the example files from this repo into that folder (adjust paths if you run the command from a different location):

```powershell
Copy-Item -Path .\fastfetch\* -Destination "$env:USERPROFILE\.config\fastfetch" -Recurse -Force
```

Or paste the files manually into `%USERPROFILE%\.config\fastfetch`.

5. Verify

- Run `fastfetch` in the terminal to verify it shows your custom ASCII clover and info:

```powershell
fastfetch
```

## Customization tips

- Change the ASCII art: edit [fastfetch/ascii.txt](fastfetch/ascii.txt) to replace the clover or add new ASCII art.
- Fastfetch config: edit [fastfetch/config.jsonc](fastfetch/config.jsonc) to change colors, modules, order, and enable/disable sections.
- Terminal settings: tweak [Comand Prompt/settings.json](Comand%20Prompt/settings.json) to change font, color scheme, background, and startup behavior.
- PowerShell profile: add aliases, environment variables, or automatic `fastfetch` execution in [PowerShell/profile.ps1](PowerShell/profile.ps1) or your `$PROFILE` file.
- Multiple ASCII sets: create multiple ASCII files in `%USERPROFILE%\.config\fastfetch` and point your `config.jsonc` at the desired file.

## Troubleshooting

- `winget install fastfetch` may fail if the package id differs; install manually from the project's releases.
- If you don't see hidden folders in Explorer, enable "Hidden items" or use `dir /a` in PowerShell.
- Ensure `fastfetch` is on your PATH; reopen your terminal after installation.

## Done

After these steps, your Command Prompt should display Fastfetch output with the clover ASCII art.
