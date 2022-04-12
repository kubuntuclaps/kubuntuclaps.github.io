---
title: "Cracking series #2: Steam games"
date: 2022-04-10
tags: ["cracking", "reversing", "asm", "ida", "debugger", "steam"]
description: "Hi! In the previous chapter we tried to crack a CD protected game, which i failed in the attempt so, i really wanted to crack myself this game so i had a good idea..."
---

Hi! In the previous chapter we tried to crack a CD protected game, which i failed in the attempt so, i really wanted to crack myself this game so i had a good idea...

I had bought the game on steam, so why not crack the steam version? Don't waste any more time and let's get started.

# Files

I created a copy outside of steamapps folder (in case of something bad happens) and closed my steam session. We have 2 EXEs again, AppLauncher.exe and Sonic Adventure DX.exe.

When you try to open one of these it will open steam and (in the case of you dont have bought the game) redirects you to the steam store to purchase the game...

Well, if you ever downloaded a cracked game, you know that steam has a API that gives developers some functions like archivements, multiplayer, and this protection (which is actually bad and we'll talk later about it). That's steam_api.dll

![](/assets/img/cracking-series-2/sonic_files.png)

We can talk about do difficult things like Steam API emulation but let's dig into the basic reverse engineering process.

# Reversing AppLauncher.exe

Like before in this file we do not have any kind of EXE alteration so we can read the asssembly code as always.

We find a WinMain function that by the name we can understand that's the one which creates the configuration window. I set some breakpoints in things that seems interesting and start debugging.

![](/assets/img/cracking-series-2/launcher_graph.png)

When hitting the SteamManager breakpoint, steam opens up and tells you to buy the game... Hmm interesting, let's JUMP directly into the other function and see what happens.

![](/assets/img/cracking-series-2/launcher_video.gif)

Boom!! Now we can open game's launcher without steam! But let's not sing victory like last time XD.

Let's take a closer look at the other file (Sonic Adventure DX.exe) and the most important because is the game itself...

# Reversing Sonic Adventure DX.exe

Opening in IDA and waiting for the auto analysis we found this.

![](/assets/img/cracking-series-2/sonic_graph.png)

Again we found a WinMain function with some interesting code, like checking if another game of Dreamcast Collection (to which this game belongs). But as we know how steam works, let's search for SteamManager in strings.

![](/assets/img/cracking-series-2/sonic_steammanager.png)

After following some XREFs, we finally find where this function is being used... So let's analyze the flow of both references.

![](/assets/img/cracking-series-2/sonic_first_xref.png)

In the first reference, we can find a conditional jump that separates the part when SteamManager is called (so game checks if you have the game) and the rest of code.

![](/assets/img/cracking-series-2/sonic_second_xref.png)

Again we see the same stuff, so let's change it to a normal JUMP and set some breakpoints...

![](/assets/img/cracking-series-2/sonic_video.gif)

Yaay!! We successfully cracked our first game, it's working without steam.

# Final note

I'm very surprised about game developers doesn't use more protection like packing, anti-debugging and a large etcetera in the main EXE. In the next episode, i will teach you how to crack a lot of steam games with a simple step... Stay tuned.

