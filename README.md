<p align="center">
    <img src=".github/xcolor-demo-v2-rounded.gif" alt="Demo" width="400"/>
</p>

# Xcolor

Change \*nix colorschemes on the fly ✈️ written in pure POSIX sh

## How does it work?

Xcolor comes in two parts: editing Xresources to include a configuration file which defines all the colors for the selected theme, and dynamically reloading all TTYs to the correct colors via escape sequences.

Once Xresources contains the proper environment variables, the database is reloaded along with any bars, WMs / DEs, etc the user is using.

Unfortunately, this change will only effect terminals opened after this point. To get currently open terminals to update, escape sequences are used. A file with the necessary sequences is generated and placed in `$XDG_CACHE_HOME` before being sent to each open terminal instance.

## Will it work on my system?

Xcolor is confirmed working with the following configurations:

Terminal Emulators:

* `urxvt`
* `xterm`
* `st` (requires xresources patch)
* `xst`
* `termite`

WMs/DEs:

* `i3`
* `sway`
* `bspwm`

Bars:

* `polybar`

This list will be updated as more configurations are tested.

Certain terminal emulators inherently will not allow you to source the colorscheme from `.Xresources`. One approach to get around this, as is used in [dylanaraps pywal utility](https://github.com/dylanaraps/pywal), is to put the following line in your `.bashrc`, `.zshrc`, etc:

`(cat ~/.cache/xcolor/xcolor.sequence &)`

## How do I get it?

First-time installation procedure:

```bash
git clone https://github.com/grahamsider/xcolor.git
cd xcolor
./install
./xcolor [options]
```

## How do I make my own themes?

Xcolor now supports over 200 themes!

To create your own, simply a copy of the template (located at `themes/template`) and edit the hex color values to your liking. When you're finished, just copy it to `$XDG_CONFIG_HOME/xcolor/themes` and you're good to go!

## How do I use these colors in other programs?

### Polybar

Polybar can source its various colors from `.Xresources` with the following syntax:

`${xrdb:XRESOURCE-COLOR:FALLBACK-COLOR}`

Example:

```ini
; Set background and foreground colors
background = ${xrdb:color0:#ffffff}
foreground = ${xrdb:color15:#ffffff}
```

### i3

i3 allows you to source resources into variables via the `set_from_resource` keyword. The general format is:

`set_from_resource $name_for_i3 color_num backup_color`

Example:

```bash
# Set the focused window borders to bold yellow
set_from_resource $yellow_b color11 #ffffff
client.focused $yellow_b $yellow_b $yellow_b $yellow_b
```

### rofi

As of version 0.4.3, a new file will appear in the `$XDG_CACHE_HOME/xcolor` directory by the name of `xcolor.rasi`. This file may be imported into a rofi `.rasi` configuration to synchronize rofi with xcolor. To do this, add the following to the **end** of your `.rasi` config (replacing `USER` with the appropriate username):

```css
@import "/home/USER/.cache/xcolor/xcolor.rasi"
```

This file defines the current xcolor theme colors for use as `@foreground`, `@background`, `@cursor`, and `@color[0-15]`.
