---
title: '[Openbox] Pseudo Tiling - Default Settings and Bash Scripting'
date: 2019-01-04 18:34:53
tags:
  - tiling
  - archlinux
  - openbox
  - wm
  - ricing
category:
  - Linux
---

As we all know, Openbox is a floating window manager. For mouse user it maybe easy, but for me that always lazying and use laptop in my bed, it's hard to navigate, especially when i want to see multiple windows at once. That's where tiling needed. Unlike in tiling window manager, we must bind keys to tile our window, so i called it Pseudo-Tiling.

I have two ways to tile window in openbox. Using only `rc.xml` config and using bash script and bind it in `rc.xml`. Each one of them has it's pros and cons. In this article I will explain both of them.

## rc.xml

We can't really using openbox without `rc.xml`. Almost all of openbox configs are stored there, from keybind, mousebind, selected openbox theme, and many other things. And my config rely on keybind settings.

Openbox has `MoveResizeTo` action that like it's name let us move and resize window in specific location and size. It can be either represented by pixel or percent.

```xml
<action name="MoveResizeTo">
  <x>34%</x>
  <y>2%</y>
  <height>96%</height>
  <width>32%</width>
</action>
```
The configuration above will move our window to 34% from left and 2% from top of the screen, and will resize to 96% in height and 32% in width. However, it only works on unmaximized windows. To make it works on maximized windows, we must first unmaximize that window. It can be done if we add this action:

```xml
<action name="Unmaximize"/>
```

Add it above the `MoveResizeTo` action. Thus, our configuration will looks like:

```xml
<action name="Unmaximize"/>
<action name="MoveResizeTo">
  <x>34%</x>
  <y>2%</y>
  <height>96%</height>
  <width>32%</width>
</action>
```

Don't forget to bind keys or that configuration won't be applicable. In my case, I bind it to `Super+x` key.

```xml
<keybind key="W-x">
  <action name="Unmaximize"/>
  <action name="MoveResizeTo">
    <x>34%</x>
    <y>2%</y>
    <height>96%</height>
    <width>32%</width>
  </action>
</keybind>
```

Now we can tile our window to center with 1/3 monitor width if we press `Super+x`.

### Configuration
What else?

Ofcourse, we need to bind other keys like tile to left with 1/3 monitor width, etc, etc. Below is my current pseudo-tiling configuration. Add it beetween `<keyboard></keyboard>` tag.

```xml
<!-- gaps 2 windows -->
<keybind key="A-W-Up">
  <action name="Unmaximize"/>
  <action name="MoveResizeTo">
    <x>1%</x>
    <y>2%</y>
    <width>98%</width>
    <height>47%</height>
  </action>
</keybind>
<keybind key="A-W-Down">
  <action name="Unmaximize"/>
  <action name="MoveResizeTo">
    <x>1%</x>
    <y>-2%</y>
    <width>98%</width>
    <height>47%</height>
  </action>
</keybind>
<keybind key="A-W-Right">
  <action name="Unmaximize"/>
  <action name="MoveResizeTo">
    <x>-1%</x>
    <y>2%</y>
    <width>48%</width>
    <height>96%</height>
  </action>
</keybind>
<keybind key="A-W-Left">
  <action name="Unmaximize"/>
  <action name="MoveResizeTo">
    <x>1%</x>
    <y>2%</y>
    <width>49%</width>
    <height>96%</height>
  </action>
</keybind>
<!--gaps 3 windows-->
<keybind key="W-z">
  <action name="Unmaximize"/>
  <action name="MoveResizeTo">
    <x>1%</x>
    <y>2%</y>
    <height>96%</height>
    <width>32%</width>
  </action>
</keybind>
<keybind key="W-x">
  <action name="Unmaximize"/>
  <action name="MoveResizeTo">
    <x>34%</x>
    <y>2%</y>
    <height>96%</height>
    <width>32%</width>
  </action>
</keybind>
<keybind key="W-c">
  <action name="Unmaximize"/>
  <action name="MoveResizeTo">
    <x>-1%</x>
    <y>2%</y>
    <height>96%</height>
    <width>32%</width>
  </action>
</keybind>
<!-- gaps 4 windows-->
<keybind key="W-h">
  <action name="Unmaximize"/>
  <action name="MoveResizeTo">
    <x>1%</x>
    <y>2%</y>
    <height>47%</height>
    <width>49%</width>
  </action>
</keybind>
<keybind key="W-j">
  <action name="Unmaximize"/>
  <action name="MoveResizeTo">
    <x>-1%</x>
    <y>2%</y>
    <height>47%</height>
    <width>48%</width>
  </action>
</keybind>
<keybind key="W-k">
  <action name="Unmaximize"/>
  <action name="MoveResizeTo">
    <x>1%</x>
    <y>-2%</y>
    <height>47%</height>
    <width>49%</width>
  </action>
</keybind>
<keybind key="W-l">
  <action name="Unmaximize"/>
  <action name="MoveResizeTo">
    <x>-1%</x>
    <y>-2%</y>
    <height>47%</height>
    <width>48%</width>
  </action>
</keybind>
<!-- gaps 6 windows -->
<keybind key="S-W-z">
  <action name="Unmaximize"/>
  <action name="MoveResizeTo">
    <x>1%</x>
    <y>2%</y>
    <height>47%</height>
    <width>32%</width>
  </action>
</keybind>
<keybind key="S-W-x">
  <action name="Unmaximize"/>
  <action name="MoveResizeTo">
    <x>34%</x>
    <y>2%</y>
    <height>47%</height>
    <width>32%</width>
  </action>
</keybind>
<keybind key="S-W-c">
  <action name="Unmaximize"/>
  <action name="MoveResizeTo">
    <x>-1%</x>
    <y>2%</y>
    <height>47%</height>
    <width>32%</width>
  </action>
</keybind>
<keybind key="C-W-z">
  <action name="Unmaximize"/>
  <action name="MoveResizeTo">
    <x>1%</x>
    <y>-2%</y>
    <height>47%</height>
    <width>32%</width>
  </action>
</keybind>
<keybind key="C-W-x">
  <action name="Unmaximize"/>
  <action name="MoveResizeTo">
    <x>34%</x>
    <y>-2%</y>
    <height>47%</height>
    <width>32%</width>
  </action>
</keybind>
<keybind key="C-W-c">
  <action name="Unmaximize"/>
  <action name="MoveResizeTo">
    <x>-1%</x>
    <y>-2%</y>
    <height>47%</height>
    <width>32%</width>
  </action>
</keybind>
```

### Cheatsheet
Need cheat sheet?

I'll give you for free

| Key | Action |
| --- | --- |
| Super + Alt + Up | TIle window to upper half |
| Super + Alt + Down | Tile window to bottom half |
| Super + Alt + Right | Tile window to half right |
| Super + Alt + Left | Tile window to half left |
| Super + z | Tile window 1/3 to right |
| Super + x | Tile window 1/3 to middle |
| Super + c | Tile window 1/3 to left |
| Super + h | Tile window 1/4 to top right |
| Super + j | Tile window 1/4 to top left |
| Super + k | Tile window 1/4 to bottom right |
| Super + l | Tile window 1/4 to bottom left |
| Super + Shift + z | Tile window 1/6 to top right |
| Super + Shift + x | Tile window 1/6 to top middle |
| Super + Shift + c | Tile window 1/6 to top left |
| Super + Control + z | Tile window 1/6 to bottom right |
| Super + Control + x | Tile window 1/6 to bottom middle |
| Super + Control + c | Tile window 1/6 to bottom left |

### Pros:
  - Fast
  
  It will respond right away after we press the shortcut.
  
  - Fluid
  
  Because we use percent, if we change our resolution or project our monitor to different monitor, the size and placement of the window won't be awkward.
  
### Cons:
  - Margin changed when given different resolution
  
  While using percent can make our window resizing fluid. It will break the grid margin. 


## grid

With that limitation, Twily has made a script to tile windows into grid using wmctrl and xdotool in bash scripting. You can download it [here](http://twily.info/scripts/grid#view). The advantages is that it will give you constant margin . You can easily change it from within the script. It will also works with other NETWM compilant window manager.

However, the default script has a disadvantage. The width and height of the monitor is hardcoded into the script. We don't want that, right? We want it to follow the current resolution, so when go to portrait mode, the tiling will also working great.

You can add and change few lines of code to achieve that. First we get the current resolution with `xrandr`, add code below after `if [ "$WNAME" == "Desktop" ]; then exit 3; fi` line

```bash
RES=$(xrandr --query | grep ' connected' | grep -o '[0-9][0-9]*x[0-9][0-9]*[^ ]*' | sed -r 's/^[^0-9]*([0-9]+x[0-9]+).*$/\1/')
```

In my 1600x900 resolution, the `RES` variable will return `1600x900`, and if i use portrait mode it will return `900x1600`. After that we need to change `W` and `H` variable so it get the resolution correctly.

```bash
W=$(echo $RES | cut -d "x" -f 1)
H=$(echo $RES | cut -d "x" -f 2)
```

Thats it! I know the execution time will drastically longer, in my case from 0.002 seconds into 0.240 seconds. But, hey, i'm using traditional harddisk in my machine. It shouldn't be that long with modern machine that use SSD (wish i can buy it soon :D ). Right now, i'm only using grid method so i can bind other key to other task.

Thanks for reading!