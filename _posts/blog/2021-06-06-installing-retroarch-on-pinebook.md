---
layout: post
title: "Installing retroarch on Pinebook Pro"
categories: blog
excerpt: "How to enjoy some retro-graming on an ARM64-based Pinebook Pro"
tags: [gaming, linux, arm64]
author: hlgr360
share: true
---

A quick recipe for installing [retroarch](https://www.retroarch.com/) on an ARM64-based [Pinebook Pro](https://wiki.pine64.org/wiki/Pinebook_Pro).

One of the unintended consequences of life during Corona is that I found myself sufficiently motivated to check out some of the new platforms around Open-Source hardware. Since I have become more and more disappointed about the direction Apple is taking my Macbook Pro war horse plus being having more and more mandatory compliance software running on my work machine plus learning that `surveilance capitalism` even extends to premium hardware sellers like Apple and friends (read this [well-balanced article](https://9to5mac.com/2020/11/15/apple-explains-addresses-mac-privacy-concerns/)), I decided to invest in my first new Linux laptop in probably 10 years. But I wasn't ready to throw in the big bucks just yet, but wanted to start with something small to get my feet wet. I figured that if it would work for my most common work tasks, it could provide some initial untethering from the constant surveillance we are subjected to.

So I ordered a [Pinebook Pro](https://www.pine64.org/pinebook-pro/) and was blown away by the quality of the device I received. Having been burnt by a previous version of the `Macbook Air` and the Butterfly Keyboard desaster on my Macbook Pro, I received a solidly built ultra-light laptop with metal casing and very pleasant tactile keyboard with a battery uptime of 10+ hours. have I mentioned that the machine costs 200$? 

You have to be realistic what you will get for a price like this - this is not a Race Horse, but a dependable Mule .. tough and solidly built, with a certain beauty in its limitations and constrains, a solid developer laptop if you are like me mostly writing code locally and deploying into the cloud.

Getting used to Manjaro and Arch Linux took some time - but if you are not willing to be the change, then you are just a passenger on life's journey, and not its driver (as to missquote some car advertisment from years ago).

My first project was getting Minecraft to run - while the stock Minecraft does not work, I finally got it up and running using MultiMC. Feeling empowered I wondered how much retro-gaming milage I can get from this machine, especially in comparison to an RPi3 (which has been powering my standalone retro gaming console and hand-held for the last couple of years).

The installation process turned out to be a bit more involved than I had anticipated, hence I felt that some other folks might appreciate a simple recipe to follow along (and yes, I am using yay, but just replace yay with pacman and you should be able to tag along just fine):

* (Optionally) Install a XBox-360 controller driver, run `yay -S xboxdrv-git`
* Install retroarch: `yay -S retroarch`
* Install asset packs to fix the UI (and yes, have this as second step after installing retroarch): `yay -S retroarch-assets-xmb retroarch-assets-ozone`
+ Start retroarch from the command line to get the controller setup:
  * Go to Main Menu / Online Updater / Update Controller Profile
  * You XBox 360 controller should now work - you can use it to navigate the menus
  * Exit retroarch
* Install the libretro core dependency: `yay -S libretto-core-info`
* Install the Doom core: `yay -S libretro-prboom-git`
* Start retroarch from the command line to install Doom wad:
  * Go to Main Menu / Online Updater / Content Download
  * Navigate to Doom and select it - it will give the choice to download a couple of files - download both
  * Go to Main Menu / Select Core - you should see `prboom` - select it (lower left the core should be shown as loaded)
  * Go to Main Menu / Load Content / Downloads / Doom - select one of the two
  * Select `Run`

Thats it - you should now see the familar (well, at least to my generation) Doom launch screen. Congrats and now go forth and clear out some of those bad guys from the hangar.

There is one gotcha if you want to install the PSX (Rearmed) libretro core. That core will fail to install because it wants to overwrite a file owned by `libretro-core-info`. The fix is quite simple:

* Delete the offending file manually: `sudo rm -rf /usr/share/libretro/info/pcsx_rearmed_libretro.info`
* Install the PSX (rearmed) core: `yay -S libretro-pcsx-rearmed`

I have tested the follwowing cores: `libretro-prboom-git`, `libretro-ppsspp-rbp`, `libretro-snes9x`, and `libretro-pcsx-rearmed`. I am getting a black screen trying `libretro-parallel-n64-git`, which apparently is related to the retroarch shaders, which I have not been able yet to get it fixed. :(

Thats it - now may the force be with you and play some Doom, will'ya?
