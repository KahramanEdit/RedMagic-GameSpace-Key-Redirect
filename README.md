# RedMagic GameSpace Key Redirect

Remap the RedMagic GameSpace side key to launch **any app you choose**, from a small KernelSU WebUI.

A tiny root module for the **RedMagic 11 Pro** (REDMAGICOS 11, Android 16). No APK, no background service, no daemon: the module only writes the same system settings that the stock key assignment screen uses.

## Features

- Pick any installed app by package name (e.g. `com.whatsapp`) and bind it to the GameSpace side key
- One-tap shortcut to the stock **Key Assignment** settings screen
- Remembers your last target and shows it again when you reopen the WebUI
- English / Turkish interface (flag toggle) with dark / light theme
- Zero runtime footprint: nothing runs in the background

## Requirements

- RedMagic 11 Pro (developed on NX809J, REDMAGICOS 11)
- Root with **KernelSU** (WebUI support) or **Magisk** with a WebUI host app such as KsuWebUI

## Installation

1. Download the latest `redmagic_gamespace_key_vX.Y.zip` from the [Releases](../../releases) page.
2. Flash it in KernelSU Manager or Magisk.
3. Reboot (recommended).
4. Open the module's **WebUI** (KernelSU Manager > Modules > tap the module's action/WebUI button).

## Usage

1. Open the WebUI.
2. Enter the target app's package name, for example `com.whatsapp`.
3. Tap **Save**.
4. Press the GameSpace side key. The chosen app should launch.

To change the target later, just enter a new package name and save again.

> **Tip:** If you do not know an app's package name, you can find it with
> `pm list packages | grep <name>` in a root shell, or from the app's Play Store URL (`?id=...`).

### Key Assignment shortcut

**Open Key Assignment Settings** launches the stock screen (`com.zte.settings.utility.sidekey.NewSideShortcutSettings`) so you can check or change the key function manually.

## How it works

When you save a plain package name, the WebUI runs two root commands:

```sh
settings put system fourth_physical_key_function_value 16
settings put system physical_key_function_app_value <package>
```

The first sets the side key function, the second sets which app it opens. The target is also stored in `/data/adb/gamespace_target.txt`.

Input in `package/activity` form is stored in that file only; it is **not** applied to the system settings.

## Files and state

| Path | Purpose |
| --- | --- |
| `webroot/index.html` | WebUI |
| `webroot/lang/en.json`, `webroot/lang/tr.json` | Translations |
| `/data/adb/gamespace_target.txt` | Last saved target |
| `/data/adb/redmagic_gamespace_lang.txt` | Selected UI language |
| `/data/adb/redmagic_gamespace_theme.txt` | Selected UI theme |

## Uninstall

Remove the module in your root manager and reboot. To restore the original key behavior, open **Key Assignment Settings** and pick a different function. You can also delete the files in `/data/adb/` listed above.

## Notes

- The system setting keys are specific to REDMAGICOS / ZTE firmware. Other devices or ROMs are not supported and may behave differently.

## Related

Split out of RedMagic RGB Control Center, so the RGB module only handles lighting.

## Credits

Made by Clenix with help from Claude.
