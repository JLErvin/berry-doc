---
title: Usage
has_children: false
nav_order: 4
---

# Usage

---

### Basic

`berry` does not handle keyboard input on its own.
Instead, a program like `sxhkd` is needed to translate keypress events
into `berryc` commands.
The window manager can be controlled via the following commands:

### Example
```python
# Moves the current client by 10 in the x and y direction
berryc move_relative 10 10 
```

### Commands
* `window_move`*`x y`*
    * move the focused window by x and y pixels, relatively
* `window_move_relative`*`x y`*
    * move the focused window to position x and y
* `window_resize`*`x y`*
    * resize the focused window by x and y pixels, relatively
* `window_resize_relative`*`x y`*
    * resize the focused window by x and y
* `window_raise`
    * raise the focused window
* `window_monocle`
    * set the focused window the fill the screen, respecting top_gap, maintains decorations
* `window_close`
    * close the focused window and its associated application
* `window_center`
    * center the focused window, maintains current size
* `switch_workspace`*`i`*
    * switch the active desktop
* `send_to_workspace`*`i`*
    * send the focused window to the given workspace
* `fullscreen`
    * toggle fullscreen status of the focused window, fills the active screen
* `fullscreen_state`
    * toggle fullscreen status of the focused window, doesn't resize the window
* `snap_left`
    * snap the focused window to fill the left half of the screen
* `snap_right`
    * snap the focused window to fill the right half of the screen
* `cardinal_focux`*`1/2/3/4`*
    * shift focus to the nearest client in the specified direction
* `toggle_decorations`
    * toggle decorations for the focused client
* `cycle_focus`
    * change focus to the next client in the stack
* `pointer_focus`
    * focus the window under the current pointer (used by `sxhkd`)
* `smart_place`*`true/false`*
    * place newly created clients using `berry`'s DP placement algorithm
* `draw_text`*`true/false`*
    * set whether or not text is draw in window title bars

