If you don't have the original disc based version want to generate the `thyme.exe` to load the dll automatically anyway you will need to apply a patch to the executable in your existing install of Zero Hour.

We provide patches for the 1.04 English disc version, The First Decade version and the Origin version with Bibbers fixed launchers applied. You will need one of these to proceed.

First, go [here](https://github.com/jmacd/xdelta-gpl/releases/tag/v3.0.11) to get xdelta3. Pick the x86_64 version if you are on 64bit Windows, pick i686 if you are on 32bit or aren't sure. Unzip the executable from it to the patches directory. If the directory doesn't exist, make sure you have a recent copy of Thyme.

Then copy `generals.exe` from your The First Decade install or your Origin install with Bibbers fixed launchers to the patches directory as well. If you are doing this from the CD version, then you want `game.dat` instead of `generals.exe` to be copied across.

Now you need to open cmd.exe as you need to apply the patch using the command line. You will need to navigate to the patches directory using the `cd` command and then enter the following command:

```
xdelta3-3.0.11-x86_64.exe -d -s generals.exe patch_bibber.delta thyme.exe
```

If you are patching The First Decade, then use `patch_tfd.delta` instead of `patch_bibber.delta`.

If you are patching the CD version then use `game.dat` instead of `generals.exe` and `patch_104_eng.delta` instead of `patch_bibber.delta`.

This should result in `thyme.exe` being generated in the patches directory. You can copy this back to your Zero Hour install directory and provided you also have a build of the `thyme.dll` file you should be able to run the game from `thyme.exe`.
