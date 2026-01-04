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
	- *Highly recommend going through the contents in the settings.json file (both from this repo and your own terminal's one) and only adding parts that are necessary*

- This file controls:
	- Font (JetBrains Mono recommended)
	- Color scheme
	- Transparency and padding
	- Cursor style

*Restart Windows Terminal after saving.*


**5. Configure PowerShell profile**

Check your PowerShell profile path:

```powershell
$PROFILE
```
- If it doesn’t exist:

	```powershell
	New-Item -Path $PROFILE -ItemType File -Force
	```

	Edit it:

	```powershell
	notepad $PROFILE
	```
	or

	```powershell
	code $PROFILE
	```

	Paste the contents of:

	```powershell
	PowerShell/profile.ps1
	```

- If it already exists:

	In the existing file, beneth the existing code, paste the contents of:

	```powershell
	PowerShell/profile.ps1
	```

	**Warning:** Do not erase the existing contents of the .ps1 file or rename it. You might break your profile

This profile:
- Forces UTF-8 input/output
- Clears the screen on startup
- Runs Fastfetch automatically using the custom config


**6. Verify**

Open a new PowerShell or Command Prompt window.

You should immediately see:
- Custom ASCII art
- System info from Fastfetch
- Correct Unicode rendering

*Manual test:*

```powershell
fastfetch -c "$env:USERPROFILE\.config\fastfetch\config.jsonc"
```


## Customization tips

- Edit the ASCII art: edit [fastfetch/ascii.txt](fastfetch/ascii.txt)
	- Go to [ASCII Art Archive](https://www.asciiart.eu/image-to-ascii)
	- Upload your logo/image
	- Get your ASCII art according to your own customization
- Fastfetch layout & colors configuration: edit [fastfetch/config.jsonc](fastfetch/config.jsonc)
	- change colors ($1 - $9 are the colors just change the hex code), modules, order, and enable/disable sections.
- Terminal look & feel config: edit [Comand Prompt/settings.json](Comand%20Prompt/settings.json)
	- change font, color scheme, background, and startup behavior accordinmg to your wish
	- I have used Catppuccin Mocha theme, JetBrains Mono font with 10 font size, etc.
- PowerShell profile/Startup behavior: edit [PowerShell/profile.ps1](PowerShell/profile.ps1)
	-  add aliases, environment variables, or automatic `fastfetch` execution in your `$PROFILE` file.


## Troubleshooting

- If the `winget` command fails, download and install Fastfetch directly from the project’s releases.
- `fastfetch` not found → Ensure it’s installed and on PATH. Restart terminal.
- IIf hidden folders are not visible in File Explorer, enable **Hidden items** or list them using`dir /a` in PowerShell.
- Config not applied → Confirm path exists:
	```powershell
	%USERPROFILE%\.config\fastfetch\config.jsonc
	```
- Broken characters → UTF-8 setup in profile is required.
- Remember to change your username in the files, we have used Admin as a placement


## All set then

After completing these steps, your Command Prompt will display Fastfetch output along with your custom ASCII art.


## Special Thanks

Special thanks to my friend for giving me the idea and guiding me throughout the setup.  
You can check out his profile here: [Arefin994](https://github.com/Arefin994)
