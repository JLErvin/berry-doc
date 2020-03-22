---
title: Configuration
has_children: false
nav_order: 3
---

# Configuration

### Basic

`berry` is configured via its command-line client: `berryc`.
Upon startup, `berry` will attempt to run the `autostart` file located by default
in `XDG_CONFIG_HOME/berry/autostart`.
A sample autostart has been included to help you.

Note that `berry` can be configured at runtime by running any `berryc` command.

The following are a list of `berryc` commands that affect the internal state of `berry`'s config.
To use any of these, simply prepend the command `berryc` followed by the command and it's respective arguments.

### Example
```python
#Sets the color of the inner border for the focused window to white
berryc inner_focus_color ffffff
```

### Commands
* `focus_color`*`XXXXXX`*
    * Set the color of the outer border of the focused window
* `unfocus_color`*`XXXXXX`*
    * Set the color of the outer border for all unfocused windows
* `inner_focus_color`*`XXXXXX`*
    * Set the color of the inner border and the titlebar of the focused window
* `inner_unfocus_color`*`XXXXXX`*
    * Set the color of the inner border and the titlebar of the unfocused window
* `text_focus_color`*`XXXXXX`*
    * Set the color of the title bar text for the focused window
* `text_unfocus_color`*`XXXXXX`*
    * Set the color of the title bar text for all unfocused windows
* `set_font` **`font_name`**
    * Set the name of the font to use (e.g. `set_font dina-9`)
* `border_width`*`X`*
    * Set the border width, in pixels, of the outer border
* `inner_border_width`*`X`*
    * Set the border width, in pixels, of the inneer border
* `title_height`*`X`*
    * Set the height of the title bar, does not include border widths
* `top_gap`*`X`*
    * Set the offset at the top of the monitor (usually for system bars)
* `edge_gap`*`TOP`**`BOTTOM`**`LEFT`**`RIGHT`*
    * Set the edge gap around the monitor (must include all parameters)
* `draw_text`*`true/false`*
    * Determine whether or not text should be draw in title bars
* `smart_place`*`true/false`*
    * Determine whether or not newly placed windows should be placed in the largest available space.
* `save_monitor`*`i`**`j`*
    * Associate the ith monitor to the jth workspace
* `json_status`*`true/false`*
    * Determine whether or not `BERRY_WINDOW_STATUS` returns JSON formatted text.
* `name_desktop`*`i``name`*
    * Name the `i`th desktop `name`. Used with `_NET_DESKTOP_NAMES`.
* `manage`*`Dialog|Toolbar|Menu|Splash|Utility`*
    * Set `berry` to manage clients of the above type. Clients which are managed will be given decorations and are movable by the window manager. This is not retroactive for current clients. Only Toolbars and Splahes are not handled by default.
* `unmanage`*`Dialog|Toolbar|Menu|Splash|Utility`*
    * Set `berry` to not manage clients of the above type. 
* `decorate_new`*`true/false`*
    * Determine whether or not new windows are decorated by default

Please note that for the previous commands, *`XXXXXX`* represents a hex color **without** the leading #.

All of these commands can be viewed on your system via `man berryc`.
