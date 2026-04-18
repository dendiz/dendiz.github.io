---
{"dg-publish":true,"permalink":"/key-pulse/","dg-note-properties":{"date":"2024-12-10"}}
---


KeyPulse is my take on a key press and mouse click counter. I have been tracking my keyboard usage using WhatPulse and WorkRave since around 2006.
I remember averaging 50K presses per day at one point which seems insane! I think most of my communication was online via my computer as smart phones
and messaging apps were not as prevalent at the time which contributes a lot towards that count. When I started programming on Apple platforms
I though that it would be cool to write my own counter. This is a great app to write yourself because:

- You are sure that it's only the number of keys that are being counted and not the actual keys you press and the order in which you press them. 
- You can install this type of software on a corporate computer because you are the person who wrote it.

It's actually a very simple app that sits in the menu bar

[![Screenshot-2026-02-18-at-7.19.12PM.md.png](https://img.dendiz.xyz/images/2026/02/18/Screenshot-2026-02-18-at-7.19.12PM.md.png)](https://img.dendiz.xyz/image/EimF)

- Every time you press a key it will increment a counter that it holds in a SQLite database. 
- Every time you click, move or scroll your mouse or trackpadit will increment a counter. 
- Every time you transmit or receive bytes on the default network interface the program will count it. 

This is mostly implemented in WhatPulse and others. But the coolest and latest feature I added was to playback mechanical keyboard click sounds
each time you press a key. I recorded 20 or samples from my 2012 Das Keyboard with Cherry MX blue switches and play back a random sample when 
a key is pressed 😆 This is great because I _love_ the clickity clacking of mechanical keyboards but I don't like carrying a keyboard around, I like
the feel of the MacBook's keyboard. I also like the idea of being able to switch to a different switch sound on the fly (which I still need to implement).

Check out this video of KeyPulse clickity clacking on an Apple keyboard!

<div style="position: relative; padding-top: 177.78%;"><iframe title="KeyPulse Mech keyboard simulation" width="100%" height="100%" src="https://peertube.dendiz.xyz/videos/embed/1N6Sd88RzGbGpkjUCTmXGy?start=0s" frameborder="0" allowfullscreen="" sandbox="allow-same-origin allow-scripts allow-popups allow-forms" style="position: absolute; inset: 0px;"></iframe></div>