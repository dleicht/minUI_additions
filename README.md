# minUI Additions

## 1. Nintendo DS

### What?

[shauninman's minUI](https://github.com/shauninman/MinUI) offers a very versatile packaging system to extent it's functionality. To add additional emulators, for example. And that's exactly what this does. It adds the Nintendo DS emulator (drastic by Exophase) to minUI's range of emulators. At least for the Miyoo Mini handheld. Others may follow later.
We achieve this by packaging [steward fu's drastic release](https://github.com/steward-fu/nds) according to minUI's design philosophy.

### How?

All we need to do really is to download NDS.pak.zip from the latest [release](https://github.com/dleicht/nds_minui/releases/latest). Unzip and drop it unto your Miyoo Mini sd card, so it will end up as:
`/SDCARD/Emus/miyoomini/NDS.pak/`

All your legally owned NDS roms go into: `/SDCARD/Roms/Nintendo DS (NDS)`

> [!IMPORTANT]
> In order to get sound working in drastic you need to do one more thing!

The Miyoo Mini uses a software fix called *audiofix* that's supposed to address crackling and popping noises. Unfortunately that fix doesn't work too well with drastic. According to [issue 36](https://github.com/steward-fu/nds/issues/36) we need to do two things to get proper sound output in drastic. **Luckily the NDS.pak.zip file you downloaded earlier already includes one of these, so all that's left to do is this:**

Edit `/SDCARD/.system/miyoomini/paks/MinUI.pak/launch.sh` to look like this (disabling this part of the code):
```
# if $IS_PLUS; then
# 	/customer/app/audioserver -60 & # &> $SDCARD_PATH/audioserver.txt &
# 	export LD_PRELOAD=/customer/lib/libpadsp.so
# else
#	 if [ -f /customer/lib/libpadsp.so ]; then
#	     LD_PRELOAD=as_preload.so audioserver.mod &
#	     export LD_PRELOAD=libpadsp.so
#	 fi
# fi
```

## 2. Arcade Systems

### What?

You may have noticed this already: emulating arcade games can be a painful experience. And there are many reasons why that may be the case. I believe that's why Shaun doesn't include this in the official minUI releases: because it would probably cause significant backlash he wouldn't want to be bothered with. And we can't blame him for that. After all a lot of this is hit or miss.
So don't expect me to put a games compatibility list up here... i'll open the door, you do the math :)

Essentially we need to do two things:
1. load a libretro core that works well with minarch
2. load a game rom that works with that core

Yeah, how hard can that be, right?

Talking about arcade emulation there are 3 names you probably heard of:
1. [MAME](https://www.mamedev.org/)
2. [Final Burn Alpha](https://www.fbalpha.com/)
3. [Final Burn Neo](https://github.com/finalburnneo/FBNeo)

They are supposed to do the same thing, more or less, but are actually very different from one another.

Depending on which of these you would want to use for your emulation purposes, you would need to arrange your game roms in an appropriate fashion. **Basically meaning that, for example, a game rom that's meant to be played with MAME doesn't necessarily work with Final Burn Alpha and vice versa.** And this is where things start to get complicated.

**You need the correct roms, tailored to your emulation core!**

This is why different versions of game roms are being put into different romsets. So you would know what kind of an emulation framework they are supposed to work with.

I mean arcade emulation was already a thing in [miniUI](https://github.com/shauninman/MiniUI-Legacy-Miyoo-Mini) (minUI's predecessor). Not officially, [but it did work](https://github.com/tiduscrying/MiniUI-Extra-Extras). So what's the difference with minUI?

miniUI did use a [port](https://github.com/shauninman/picoarch) of neonloop's [picoarch](https://git.crowdedwood.com/picoarch/) as the emulation/libretro framework. Itself picoarch makes use of [libpicofe](https://github.com/notaz/libpicofe) by the one and only notaz (*bows in utmost respect*). Inspired by picoarch Shaun later developed his own minarch.

As was shown earlier, picoarch did support the Final Burn Alpha (fbalpha) libretro cores. Unfortunately minarch doesn't anymore. Loading the fbalpha core in minarch results in a segfault, at least on my devices. So this means emulating arcade games with fbalpha doesn't work on minUI. I believe that's caused by some missing library shenanigans, but who knows. Doesn't make sense to sink lots of time in debugging this, since there already is a (better) working alternative already: **Final Burn Neo**.

It is a bit weird, because you probably keep reading that fbalpha is supposed to give better performance on low spec devices like the miyoo mini. So, just like me, you may have never given fbneo much thought.

Wait wait wait... what about MAME? There are libretro cores for that, why not use MAME instead? True. And they do work with minarch. But they don't perform as well as fbneo.

### How?

All we need to do really is to download FBN.pak.zip from the latest [release](https://github.com/dleicht/nds_minui/releases/latest). Unzip and drop it unto your Miyoo Mini sd card, so it will end up as:
`/SDCARD/Emus/miyoomini/FBN.pak/`

All your legally owned arcade roms go into: `/SDCARD/Roms/Arcade (FBN)`

> [!IMPORTANT]
> You need to make sure to use roms that are meant to work with Final Burn Neo!

## 3. Troubleshootin'

These .paks are configured to write log files to `/SDCARD/.userdata/miyoomini/logs/`

Find the .txt files there and try to figure out what the issue may be.
