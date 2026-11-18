# regoldsrc

a goldsrc-compatible engine with a bunch of fixes and perf work on top.

## build

you need:

- visual studio (msvc, x86 / win32)
- cmake
- vsyasm (drop yasm.exe next to the msvc toolchain)

```
cmake -S . -B build -A Win32
cmake --build build --config Release
cmake --install build --config Release
```

install drops the binaries (hw.dll, sw.dll, GameUI.dll, ...) into game/.
game/ and build/ are not tracked here.

## whats in here

fixes:

- options menu / vgui crash
- save/load crash (also the sp death -> respawn reload crash)
- mp accessory (cape/hat) flicker
- fullscreen zoom/crop + menu click offset at 125% windows scaling
- dpi awareness + real gl drawable size handling
- bounds / overflow hardening on a few server-input paths
- bundled sdl2 bumped 2.0.0 -> 2.32.10

perf:

- mdl (studio) model renderer rewritten to vbo batching (one gldrawelements per pose, cvar gl_mdl_vbo)
- attached / follow models (hats, capes, weapons) no longer re-evaluate the player skeleton for every sibling
- r_studiomergebones uses a hash pre-filter instead of o(bones^2) strcasecmp
