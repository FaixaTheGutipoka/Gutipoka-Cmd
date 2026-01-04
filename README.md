# Gutipoka CMD

A concise guide to set up CloverCmd appearance using Fastfetch and a custom Command Prompt/PowerShell configuration.

## Overview

This repo contains example settings and Fastfetch files used to give Command Prompt a Clover-themed prompt (ASCII clover). Follow the steps below to reproduce the setup.

## Screenshot

Below is a screenshot of my Command Prompt showing the Clover ASCII and Fastfetch output:

![CloverCmd screenshot](screenshot.png)


## Files in this repo
- [Comand Prompt/settings.json](Comand%20Prompt/settings.json)
- [fastfetch/ascii.txt](fastfetch/ascii.txt)
- [fastfetch/config.jsonc](fastfetch/config.jsonc)
- [PowerShell/profile.ps1](PowerShell/profile.ps1)

## Steps

1. Paste the Command Prompt settings

- Open Windows Terminal or Command Prompt settings and paste the JSON from:
  - [Comand Prompt/settings.json](Comand%20Prompt/settings.json)

2. Install Fastfetch

Run:

```powershell
winget install fastfetch
```

If that package name doesn't match in `winget`, install Fastfetch from its official repo or releases page and ensure `fastfetch` is on your PATH.

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
