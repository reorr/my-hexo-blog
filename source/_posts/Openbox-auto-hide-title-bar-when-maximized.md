---
title: '[Openbox] auto hide title bar when maximized'
date: 2019-01-02 20:13:11
tags:
  - archlinux
  - openbox
  - wm
  - ricing
categories:
  - Linux
---

<div align="center">

![auto-hide-title-bar header-image](/images/posts/auto-hide-header.png)

</div>

## Prelude
Recently i'm stumbled upon something. It's an urgent matter. In my current openbox setup, I'm using vala-appmenu-plugin in xfce panel. The reason is simple, i want to get more space without losing important information from my panel like netspeed, notification, and other important things. With appmenu-plugin i can get rid menubar on all over my apps and get that tiny space back, but i'm not satisfied. That title bar under my panel looks so ugly.

![ugly-title-bar-on-maximized](/images/posts/ugly-title-bar-on-maximized.png)(Read JoJolion, thanks)

## The openbox things
In openbox we can't get rid the title bar. You can remove the border and the window action button, but that's it. Yeah, we can remove it with provided `undecorate window` action. That means i've to undecorate it everytime i maximize a window. How ridiculous! Btw, in xfce they have option to hide title bar whe maximized.

## The options
Okay, there is two tricky options that can be done by default openbox setting.

1.	Undecorate all windows when appears
2.	Toggle window decoration when maximized

The first option is not the one that i wanted. The behaviour that i want is the one in xfce, it only hide the title bar when maximized. I want to have a nice small title bar on my window when it's not maximized.
The second option also out of question. It certainly can do the job. But, duh it's complicating my `rc.xml` file. Also if a window undecorated, when it maximized, it will be decorated.

## Solution
[Orcsome](https://github.com/baverman/orcsome) is a scripting extension for NETWM compilant window managers written in python. With it we can extend wm fuctions. So, I can create script to do what I want, undecorate window when maximized and undecorate window if not maximized. Fortunately someone has write the configuration for that. Below is the configuration that i found.

``` python
from orcsome import get_wm

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
```

Copy that to `$HOME/.config/orcsome/rc.py`.

Now, what you need to do is install orcsome and run it at startup. You can install orcsome with `pip`. Because orcsome written with `python2` and archlinux that I use is using `python3` by default, I install it with `$ pip2 install orcsome` command. If you are using debian devariative, `pip` is the right command.

Here's my current wm behaviour

![auto-hide-title-bar](/images/posts/auto-hide-title-bar.gif)

## How to make everyone happy
<h3>No can do.</h3>

Source: https://dglava.github.io/en/orcsome.html