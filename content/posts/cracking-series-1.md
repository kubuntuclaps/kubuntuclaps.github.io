---
title: "Cracking series #1: CD protected games"
date: 2022-04-10
tags: ["cracking", "reversing", "asm", "ida", "debugger"]
---

Hello! Welcome to my first post, im very excited about it so let's start.

I was playing some videogames when i got curious of how games are cracked, then i downloaded an old game from my childhood... Sonic Adventure DX.

# Let's dig into it.

I downloaded the disc version from The Seven Seas website that is blocked for a lot of ISPs, after installing it without the DEVIANCE crack, i go into the game folder and find two .EXEs: autorun.exe and sonic.exe

Autorun executable gives you the choice of editing settings like game's language, display settings, and all these things. When you press play, checks if you have the game cd, otherwise it gives you an error. 

![](/assets/img/cracking-series-1/autorun_error.png)

Fine, let's do some reversing.

# Reversing autorun.exe

We know sonic.exe is the game, so searching on IDA strings the executable name and following the XREF we find something interesting.

![](/assets/img/cracking-series-1/autorun_graph.png)

Interesting, we can see first conditional jump that separates our sonic.exe between something else.

![](/assets/img/cracking-series-1/autorun_block.png)

So what's happens if i change that **JNZ** for a **JUMP**...

![](/assets/img/cracking-series-1/autorun_video.gif)

Voila! we successfully patched the inital exe of game (now the error is from sonic.exe)

# Reversing sonic.exe

As you know, i'm a beginner in reverse engineering so i wasn't able to crack this game due to the "high" security that have (SecuROM) and anti-debugging techniques.

# To finish

Here a diagram of the files

![](/assets/img/cracking-series-1/sonic_files.png)

I wasn't able to totally crack the game but... we learned something new! Not always in life we got what expect. Don't worry, in the next episode we will try to crack the same game but the steam version. Maybe this time i will be successful.

Special mention to my friend [Eternity](https://github.com/eternidades), he helped me with IDA shortcuts, usage of x32dbg, and i really appreciate.

Thanks for reading! ❤