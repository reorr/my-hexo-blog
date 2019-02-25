---
title: How To Make Xfce4-panel Behave Like Elementary OS Panel
date: 2019-02-25 20:00:31
tags:
  - ricing
categories:
  - Linux
---
By behave like Elementary OS i mean the ability to change panel opacity automatically when there any maximized windows in current workspace. I like this behavior very much, having solid panel color when in desktop dont feels aestethic for me. I will explain how my script works below.

# Get current active workspace
We can achive this with `wmctrl` command.
``` bash
$ wmctrl -d
0  * DG: 1600x900  VP: 0,0  WA: 0,0 1600x867   一 
1  - DG: 1600x900  VP: N/A  WA: 0,0 1600x867   二 
2  - DG: 1600x900  VP: N/A  WA: 0,0 1600x867   三 
3  - DG: 1600x900  VP: N/A  WA: 0,0 1600x867   四
```
The star character indicate the current active workspace. We only need current workspace number, so we must cut it
``` bash
$ wmctrl -d | grep -w "*" | cut -d" " -f 1
0
```
`grep -w "*"` command print only lines with * character in it. Then we cut it to get that workspace number.

# Get window list in current workspace

After we get the current active workspace, we can get window list with `wmctrl -l` command.
Ofcourse the output is a mess.
``` bash
$ wmctrl -l
0x00a00004 -1 Chamelemon xfce4-panel
0x00c00003 -1 Chamelemon Desktop
0x01e00009  0 Chamelemon fish in ~
0x03c00011  0 Chamelemon elementary OS 5 Juno is Here – elementary – Medium - Mozilla Firefox
0x04800002  0 Chamelemon FBReader - Toaru Majutsu no Index - Volume 18
0x0183807f  0 Chamelemon Hiburan - File Manager
0x04400006  0 Chamelemon Telegram (80759)
0x06000009  0 Chamelemon fish in ~/S/r/my-hexo-blog
0x06800001  0 Chamelemon Moeditor - How-To-Make-Xfce4-panel-Behave-Like-Elementary-OS-Panel.md
0x05e00009  0 Chamelemon fish in ~
```
Fist column indicate window id, second column indicate workspace, third column indicate hostname, and last column indicate window title. Just like the method we use to get current active workspace number, we need to eliminate lines without current workspace number, and cut it to get the first column.
``` bash
$ wmctrl -l | grep -w "0" | cut -d' ' -f1
0x01e00009
0x03c00011
0x04800002
0x0183807f
0x04400006
0x06000009
0x06800001
0x05e00009
```
There it is, we got our window id in current active workspace.

# Get window state
Wether the window is maximized or unmaximized, minimized or unminimized, it's called window state. `xprop` it a tiny utility to get those window state. You can get all those state with `xprop -id "win_id"`, change win_id with correspondent windows id that you want to see. The output is more of a mess than `wmctrl` command, so i dont print that here.

Window state that we want to get appear in `_NET_WM_STATE(ATOM)` line. We want to get state that include `_NET_WM_STATE_MAXIMIZED_HORZ` and `_NET_WM_STATE_MAXIMIZED_VERT`, but exclude `_NET_WM_STATE_HIDDEN`. Because we dont want to include the minimized windows.

# Get current panel opacity and change panel opacity

With xfconf-query we can manipulate xfce4-panel configuration easily through terminal. Type command below to get current panel opacity.
``` bash
$ xfconf-query -c xfce4-panel -p /panels/panel-1/background-alpha
100
```
The output (100) is my current panel opacity.

To manipulate that value, just add `-s` flag followed by desired value (0-100) in above command like this.
```
$ xfconf-query -c xfce4-panel -p /panels/panel-1/background-alpha -s 50
```
That command will chage the panel opacity immediately to 50%.

That's all the basic, we need to wrap it up to make a script that will do it automatically.

# Wrap the script

``` bash
#!/bin/env bash

min=40
max=100
curr_alpha=$(xfconf-query -c xfce4-panel -p /panels/panel-1/background-alpha)
curr_desktop=$(wmctrl -d | grep -w "*" | cut -d" " -f 1)
arr=()
```

min is our minimum opacity value, while max is the maximum value we want. curr_alpha variable store current opacity value of our panel. arr=() is array variable, we need it to store list of maximized windows that unminimized. curr_desktop store our current active workspace.

next.
``` bash
for i in `wmctrl -l | grep -w "$curr_desktop" | cut -d' ' -f1`; do
	exist=$(xprop -id "$i" | grep "_NET_WM_STATE(ATOM)" | grep "_NET_WM_STATE_MAXIMIZED_VERT" | grep "_NET_WM_STATE_MAXIMIZED_HORZ" | grep -v "_NET_WM_STATE_HIDDEN")
	if [ -z $exist ]; then
		echo "unmaximized"
	else
		arr[${#arr[@]}]="maximized"
	fi
done
```

We loop through all windows id that exist in our current workspace to get window state. If we got window that are maximized and unmaximized, we add item to arr variable.

``` bash
if [ ${#arr[@]} -eq 0 ]; then
	for ((i=$curr_alpha; i>=$min; i--)) ; do
		xfconf-query -c xfce4-panel -p /panels/panel-1/background-alpha -s $i
	done;
else
    for ((i=$curr_alpha; i<=$max; i++)) ; do
		xfconf-query -c xfce4-panel -p /panels/panel-1/background-alpha -s $i
    done;
fi
```

If arr variable is empty, it will set panel opacity to minimum, and vice versa. The change will done gradually creating animate effect.

Full script
``` bash
#!/bin/env bash

min=40
max=100
curr_alpha=$(xfconf-query -c xfce4-panel -p /panels/panel-1/background-alpha)
curr_desktop=$(wmctrl -d | grep -w "*" | cut -d" " -f 1)
arr=()

for i in `wmctrl -l | grep -w "$curr_desktop" | cut -d' ' -f1`; do
	exist=$(xprop -id "$i" | grep "_NET_WM_STATE(ATOM)" | grep "_NET_WM_STATE_MAXIMIZED_VERT" | grep "_NET_WM_STATE_MAXIMIZED_HORZ" | grep -v "_NET_WM_STATE_HIDDEN")
	if [ -z $exist ]; then
		echo "unmaximized"
	else
		arr[${#arr[@]}]="maximized"
	fi
done

if [ ${#arr[@]} -eq 0 ]; then
	for ((i=$curr_alpha; i>=$min; i--)) ; do
		xfconf-query -c xfce4-panel -p /panels/panel-1/background-alpha -s $i
	done;
else
    for ((i=$curr_alpha; i<=$max; i++)) ; do
		xfconf-query -c xfce4-panel -p /panels/panel-1/background-alpha -s $i
    done;
fi
```

Save as `change-panel.sh`, and dont forget to set the script as executable

``` bash
$ chmod +x change-panel.sh
```

Try to execute it in terminal while unmaximized and when maximized to see the change. Move that script to your `$PATH` directory, so you can execute it everywhere.

Now we need to run that script automatically every window event changed. Remember how i hide title bar when my windows is maximized? Yep, i'm using orcsome to listen window event. I just need to change my `rc.py` a little to looks like this

``` python
from orcsome import get_wm
import orcsome
import subprocess

wm = get_wm()

@wm.on_manage
def on_manage():
    @wm.on_property_change(wm.event_window, '_NET_WM_STATE')
    def property_was_set():
        w = wm.event_window
        if w.maximized_vert and w.maximized_horz:
            if w.decorated:
                wm.set_window_state(w, decorate=False)
        else:
            if not w.decorated:
                wm.set_window_state(w, decorate=True)
        subprocess.call(['change-panel'])
```

<h1>IT'S DONE!</h1>

Preview:
<iframe width="560" height="315" src="https://www.youtube.com/embed/qmcbkxF6mxM" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>