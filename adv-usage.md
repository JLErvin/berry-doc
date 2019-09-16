---
title: Advanced Usage
has_children: false
nav_order: 5
---

# Advanced Usage

---

## Introduction

`berry` is itself a very simple program with only a handful of commands
to manage its internal state and control active clients.
For more advanced behavior `berry` relies on users creating custom
commands and shell scripts based on its most basic features. 

To accomplish this, `berry` is compliant with a subset of `ICCCM` and `EWMH`.
Additionally, `berry` implements its own properties on the x-server
that are exposed to users.

## Internal State

On of `berry`'s most powerful features is the ability to view the internal state
of active clients.
The following is a description of useful properties on the xserver
that can be viewed via `xprop`.

* `BERRY_WINDOW_STATUS`
* `_NET_SUPPORTED`
* `_NET_NUMBER_OF_DESKTOPS`
* `_NET_ACTIVE_WINDOW`
* `_NET_WM_STATE_FULLSCREEN`
* `_NET_SUPPORTING_WM_CHECK`
* `_NET_CURRENT_DESKTOP`
* `_NET_WM_STATE`
* `_NET_CLIENT_LIST`
* `_NET_WM_WINDOW_TYPE`
* `_NET_WM_TYPE_TOOLBAR`
* `_NET_WM_TYPE_MENU`
* `_NET_WM_TYPE_SPLASH`
* `_NET_WM_TYPE_DIALOG`
* `_NET_WM_TYPE_UTILITY`
* `_NET_WM_FRAME_EXTENTS`
* `_NET_DESKTOP_NAMES`
* `_NET_DESKTOP_VIEWPORT`

## BERRY_WINDOW_STATUS

---

Each client managed by `berry` maintains a UTF8-String that documents
its geometry and state. By default, this information is reported
in a `JSON` formatted string and can be easily parsed by a program like `jq`.

To view the state of a window with id `XXXXXX`:
```bash
xprop -id 0xXXXXXX BERRY_WINDOW_STATUS
```
If you have set `json_status` to true, the following will be returned:
```bash
#JSON return
BERRY_WINDOW_STATUS(UTF8_STRING) = "{\"window\":\"0x02000009\",\"geom\":{\"x\":950,\"y\":285,\"width\":570,\"height\":680,},\"state\":normal,\"decorated\":true}"
```
To parse this using `jq`, the following would be appropriate:
```bash
#!/usr/bin/env bash

hint="$(xprop -notype -id 0x1200009 BERRY_WINDOW_STATUS)$
eval json="${hint#* = }"
jq <<< "$json"
```

This would return the entire `JSON` string and would print by `jq` as follows:
```json
}
  "window": "0x01000009",
  "geom": {
    "x": 670,
    "y": 210,
    "width": 570,
    "height": 680
  },
  "state": "normal",
  "decorated": "true"
}
```

If you have set `json_status` to be false, the following will be returned:

```bash
# KEY:                              window id    x    y    w    h   state   dec
BERRY_WINDOW_STATUS(UTF8_STRING) = "0x02000009, 950, 285, 570, 680, normal, true"
```
Values are based on the mapping described by the previous key.

