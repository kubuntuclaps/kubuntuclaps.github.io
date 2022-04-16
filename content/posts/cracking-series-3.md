---
title: "Cracking series #3: Steam multiplayer"
date: 2022-04-10
tags: ["cracking", "reversing", "asm", "ida", "debugger", "steam", "multiplayer"]
description: "Welcome to the new episode of my cracking series, today we will see how i cracked 50% (approximately) of the steam library with a simple thing."
---

Welcome to the new episode of my cracking series, today we will see how i cracked 50% (approximately) of the steam library with a simple thing. A lot of games are vulnerable to this.

# Let's get started

Well, i downloaded Sonic Generations from our seven seas website, and i see the crack is a .DLL file (steam_api.dll) which 1337 people archieve the way of emulate it (and get online functions)...

How the file works? In a simple way, it emulates steam and spoofs the GameID which is a number to identify the game XD and spoofs it into Spacewar. And you will ask, What is Spacewar?

![](/assets/img/cracking-series-3/spacewar.jpg)

This is Spacewar, a hidden steam demo for game developers that everyone has access. So crackers find the way with a custom DLL to recreate all the steam api.

Well as you can see on my other posts, i have a low knowledge in reversing, asm and C so i can't explain to you how... Wait, what if i say you i found a way to do the same without the DLL, You cant believe me right?

# Reversing Sonic Generations

Firing up IDA and doing some reversing, i can't find our SteamManager like the last episode but i found something interesting on the game's folder.

![](/assets/img/cracking-series-3/sonic_generations_files.png)

A file named steam_appid.txt, let's open it and see what contains...

```
71340
```

Interesting, at the moment when i try to open the game, is just opening a empty MessageBox, what happens if i change 71340 (Sonic Generations Steam ID) into 480, Spacewar ones.

![](/assets/img/cracking-series-3/sonic_generations_spoof.png)

Game is opening and i'm playing Spacewar (without altering DLL), well... too good to be true right? I can't press start and i'm stucked in start screen, literally i smashed my keyboard and controller :(

Well, don't worry, let's try with another game...

# Scrap Mechanic

My friend, [Migu](https://github.com/migu-star) has purchased the game, so using Steam's family option he can lend me the game... After downloading it and removing game access from my account, let's try this

It is worth noting that if the game does not have this file (as is the case with scrap mechanic), you can create it and try to run it.

![](/assets/img/cracking-series-3/scrap_mechanic_spoof.png)

Nice!! I can open the game and this time is fully playable (at least as far as I've tested)

![](/assets/img/cracking-series-3/scrap_mechanic_menu.png)

Now let's move on to multiplayer... I told Migu to create a new steam account and add me into my main, after creating a new room and invite him with the SHIFT + TAB overlay

![](/assets/img/cracking-series-3/spacewar_invite.png)

And that's, we did it guys!

![](/assets/img/cracking-series-3/scrap_mechanic_online.png)

# Closing statements

Reading on google, i found like a [documentation](https://kb.heathenengineering.com/assets/steamworks/learning/core-concepts/steam_appid.txt) of Steamworks, this file is used by Steam API and tells which ID to use. After more researching, i understand why this is not working for every single game and is because of Steamworks is not a DRM (Digital Rights Management) and is the fault of developers, because this file is used for developer testing. 

I don't think I'm going to continue this series anymore because i want to do web stuff, but it has been fun.

Thanks for reading ❤