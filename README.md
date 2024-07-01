# NDS for minUI on Miyoo Mini

## What?

[shauninman's minUI](https://github.com/shauninman/MinUI) offers a very versatile packaging system to extent it's functionality. To add additional emulators, for example. And that's exactly what this does. It adds the Nintendo DS emulator (drastic by Exophase) to minUI's range of emulators. At least for the Miyoo Mini handheld. Others may follow later.
We achieve this by packaging [steward fu's drastic release](https://github.com/steward-fu/nds) according to minUI's design philosophy.

## How?

All we need to do really is to download NDS.pak.zip from the latest [release](https://github.com/dleicht/nds_minui/releases). Unzip and drop it unto your Miyoo Mini sd card, so it will end up as:
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

