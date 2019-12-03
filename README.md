<p align="center">
    <img src=".github/xcolor-demo-rounded.gif" alt="Demo" width="540"/>
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

WMs/DEs:

* `i3`<sup>1</sup>

Bars:

* `polybar`<sup>2</sup>

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

Xcolor currently comes with 3 colorschemes pre-installed:

- Gruvbox (dark)
- Nord
- Seoul256

More will be coming in the future, but if you want to make your own in the meantime, make a copy of the template (located at `themes/template`) and edit the hex color values to your liking. When you're finished, just copy it to `$XDG_CONFIG_HOME/xcolor/` and you're good to go!

## WM, DE, and Bar Configurations

<sup>1</sup>Use the following for your polybar color configurations:

`${xrdb:COLOR-NUM:FALLBACK-COLOR}` e.g. `foreground = ${xrdb:color15:#ffffff}`

<sup>2</sup>i3 allows you to bring colors from your `.Xresources` with the `set_from_resource` keyword. You can then use this color for whatever you want in i3. The general format is `set_from_resource $name_for_i3 color_num backup_color`. For example, to set the focused window borders to bold yellow you could do the following:

```
set_from_resource $yellow_b color11 #ffffff
client.focused $yellow_b $yellow_b $yellow_b $yellow_b
```
