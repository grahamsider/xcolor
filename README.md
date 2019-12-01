# Xcolor

Change terminal colors on the fly ✈️ written in pure POSIX sh

## How does it work?

Xcolor comes in two parts: editing Xresources to include a configuration file which defines all the colors for the selected theme, and dynamically reloading all TTYs to the correct colors via escape sequences.

Once Xresources contains the proper environment variables, the database is reloaded along with any bars, WMs / DEs, etc the user is using.

Unfortunately, this change will only effect terminals opened after this point. To get currently open terminals to update, escape sequences are used. A file with the necessary sequences is generated and placed in `$XDG_CACHE_HOME` before being sent to each open terminal instance.

## Will it work on my system?

Xcolor is confirmed working with the following configurations:

| Terms | WMs/DEs |   Bars  |               Notes              |
|:-----:|:-------:|:-------:|:--------------------------------:|
|   st  |    i3   | polybar | st requires the xresources patch |

This list will be updated as more configurations are tested.

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

More will be coming in the future, but if you want to make your own in the meantime, just copy a theme (located in the `themes` directory) and edit the colors to your liking. When you're finished, just copy it to `$XDG_CONFIG_HOME/xcolor/` and you're good to go!
