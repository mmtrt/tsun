<h1 align="center">
  <img src="snap/gui/tsun.png" alt="C&C: Tiberian Sun CnCNet">
  <br />
  C&C: Tiberian Sun CnCNet
</h1>

<p align="center"><b>This is the snap for C&C: Tiberian Sun CnCNet</b>. It works on Ubuntu, Fedora, Debian, and other major Linux
distributions.</p>

<p align="center">Published for <img src="http://anything.codes/slack-emoji-for-techies/emoji/tux.png" align="top" width="24" /> with :gift_heart: by Snapcrafters</p>

## Install

    snap install tsun --edge
    snap connect tsun:process-control

([Don't have snapd installed?](https://snapcraft.io/docs/core/install))

![C&C: Tiberian Sun CnCNet](screenshot.png?raw=true "C&C: Tiberian Sun CnCNet")

## Reusing this snap

You can use this snap as a reference for creating snaps of other WINE
compatible 32-bit Windows applications or games. Here are the main
things you'll need to modify:

  * Change the meta data and `apps:` and `parts:` names from `tsun`.
  * Modify the `command:` to reference the executable the application/game should launch.
  * If you can't redistrbute the application/game use `INSTALL_URL:` to reference a web accessible installer.
  * Modify the `install_app()` and `launch_app()` functions in [`snap/scripts/sommelier`](snap/scripts/sommelier) to suit the application/game you're snapping.
  * Modify the `TITLE` and `NOTICE` in [`snap/scripts/sommelier`](snap/scripts/sommelier) to suit the application/game you're snapping.
  * If you can't redistrbute the application/game use `INSTALL_URL:` in the `environment:` of the main `command:` to reference a web accessible installer.
  * Some games require a virtual desktop to function correctly. Add `VIRTDESKTOP: 1` to the `environment:` of the main `command:` to enable virtual desktop or set it to `0` or remove it completely to disable a virtual desktop.
  * Some applications/games require that WINE DLLs are overriden, you can specify then via `DLLOVERRIDES:` in the `environment:` of the main `command:`.
  * If the application/game requires some winetricks to work then you can specify them via `TRICKS:` in the `environment:` of the main `command:`.

Here's an example `environment:` that shows how to use some of the capabilities outlined above:

```
    environment:
      WINEPREFIX: "$SNAP_USER_COMMON/.wine"
      DLLOVERRIDES: "mscoree,mshtml=" # Prevent pop-ups about Wine Mono and Wine Gecko
      INSTALL_URL: "https://downloads.cncnet.org/TiberianSun_Online_Installer.exe"
      TRICKS: "winxp corefonts d3dx9_43"
      VIRTDESKTOP: 1
      LC_ALL: "C.UTF-8"
```

One other point of interest is that `yad` is staged in the snap and a
faux `zenity` script is included that execs `yad`. We do this because
`yad` is argument compatible with `zenity` but pulls far fewer package
dependencies.

If you have any questions about creating snaps of WINE compatible
Windows applications then [post in the Snapcraft forum](https://forum.snapcraft.io).
