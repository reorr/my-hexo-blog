---
title: Developing Flutter Apps Without Phone Using Flutter Desktop Embedder
date: 2019-01-09 17:27:21
tags:
- flutter
categories:
- Programming
---

I've life without phone for about half year, since i lost my phone in bus. Not exactly without phone, my [friend](https://github.com/drzln) lend me his phone, a Samsung Galaxy Y with Android Gingerbread. Which i can't use to test my app in it. While it's don't affect my everyday life, when i need to or rather when i want to build android apps, i don't have device to test it. I can't relly on my machine, with just traditional HDD and 4GB of RAM.

A couple of days ago, my friend (the same that lend me his phone) told me about interesting project in github, [flutter_desktop_launcher](https://github.com/putraxor/flutter_desktop_launcher). This project allow us to test our app directly on desktop. It also support Hot Reload. Pretty interesting doesn't it?

But when my friend try that project, he encounter an error. It cant find a library named `libjsoncpp.so.1`. Even after installing it. At that time i haven't tried it. My guess is that it's a precompiled binary and the library version doesn't match.

Last night, after installing dark and flutter sdk, i try that project and encounter the same error. The project that hosted in github doesn't have any source code, only the binary that compressed into zip. What can i do?

After reading the README once again i click a link that linked to youtube video that demonstrate how to use the project. Voila! It turns out that he only compile it from another repository. The original repository is [flutter-dektop-embedding by google](https://github.com/google/flutter-desktop-embedding). It's time to compile it.

The instruction in README pretty much explain all step that we needs to compile the binary and library. Because i use Linux on my machine, so i must go to the `library>linux` folder and run `$ make`. After finished, we need to compile the binary. Go to `example>linux` folder. Edit the `Makefile` so the output directory is in the current directory, we don't want it to be in `out` directory and must run it with `./out/flutter_embedder_example`. After all finished, i copy the compiled library which is `lib` folder and `flutter_embedder_example` file to my `$PATH`, in my case it's in `$HOME/.bin`. Run `$ flutter_embedder_example` in terminal, and debug it via Visual Studio Code. Read [this](https://github.com/google/flutter-desktop-embedding/blob/master/Debugging.md) how to debug our app.

If you use archlinux or it's derivative, i've upload my compiled binary [here](https://mega.nz/#!7cxUTQAa!gjQxwuamxnV3Isw7NdVIv54FfIx17qgWAOJXrNMQOD4). Dont forget to run `# pacman -Syyu` because i updated my machine yesterday.

![flutter hello word in desktop](/images/posts/flutter-desktop.png)

Thanks for reading, have a decent day!