# WET Recomp - Nintendo Switch

<div align="center">
  <img src="assets/icon.png" alt="WetRecomp" width="480">
</div>

A Nintendo Switch build of [**WET**](https://en.wikipedia.org/wiki/Wet_(video_game)) (Xbox 360, Title ID `425307DB`) using ReXGlue, Vulkan, and the NVK driver.
On Switch, the Xenos GPU plugin is selected by default and Vulkan is resolved from the statically linked NVK driver.

## Requirements

- CMake 3.25+, Ninja, and devkitPro's Switch toolchain (`devkitA64` and `libnx`)
- The ReXGlue NX SDK at `../rexglue-nx-source`
- A Mesa Horizon SDK with the static NVK driver (`lib/libvulkan.a`), extracted to `../mesa-horizon-sdk`
- [extract-xiso](https://github.com/XboxDev/extract-xiso/releases) and your own copy of WET

## Game data

Extract your Xbox 360 ISO with `extract-xiso.exe -x WET.iso`, then copy the game data into `assets/` (gitignored):

```
assets/
  default.xex
  nxeart
  lu0/  lu1/
  media/  movies0/  movies1/
  streams0/  streams1/
```

## Build

```powershell
cmake --preset switch-release
cmake --build --preset switch-release --parallel 2
```

If the Mesa SDK is elsewhere, pass its `opt/devkitpro/portlibs/switch` directory when configuring:

```powershell
cmake --preset switch-release -DREXGLUE_SWITCH_NVK_SDK="D:\path\to\mesa-horizon-sdk\opt\devkitpro\portlibs\switch"
```

The NRO is `build\switch\wetrecomp.nro`. Copy it and `assets\` to the same folder on the SD card, for example `sdmc:/switch/wetrecomp/`.

## Configuration

`settings/hardware.toml` and `settings/mapping.toml` are loaded at startup. The WET options include language, frame-rate, visual-effect, and GPU-wait settings; see [`settings/README.md`](settings/README.md).

## Credits

- ReXGlue NX SDK
- [extract-xiso](https://github.com/XboxDev/extract-xiso)
