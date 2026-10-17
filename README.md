<p align="center" width="100%">

<img src="https://raw.githubusercontent.com/modestimpala/VEmu/refs/heads/main/media/vemu%20header.png">

</p>

<p align="center" width="100%">
<a href="https://discord.gg/Bq7HCMRfjk"><img width="5%" src="https://www.dropbox.com/scl/fi/96uoyd529gq617880m0cu/636e0a6a49cf127bf92de1e2_icon_clyde_blurple_RGB.png?rlkey=343xgtya1h3r53bblx8lns473&st=ih0q2alh&dl=1"></a>
</p>

Play S/NES, GB/C/A, N64, PSX/2, DOOM (yes really) and more all inside **Voices of the Void**. 

VEmu adds **libretro**-backed props into your game that let you load your own ROMs and play in-game on consoles and handhelds. All audio/video is rendered by the mod inside the game, real-time with no external windows, no lag, and full support for UE4's spatialized audio and post-processing. You do *not* need RetroArch or any other program installed to use this mod. See [Quick start](#quick-start) to get started.

Features custom models created by members of the community. PSOne, controller, and disc models by Viru. 

VEmu 1.0.0 has lots of new cool features. Please be sure to check out the CHANGELOG, and I encourage all users to try out the "Quick Menu" (Default F9) key in-game, for customizing keybinds, VEmu and core options, and more. 

Built on [libretro](https://www.libretro.com/) - Currently, the only known limits are cores that require abnormal input styles, like pure Bluetooth Wii remotes, DS touch-style input, or keyboard-only cores like DOSBox.

VEmu plays best currently with VotV FPS limited to ~60-120 and V-Sync **OFF!**

## User Data Location

```
%LOCALAPPDATA%\VEmu\ e.g. C:\Users\moddy\AppData\Local\VEmu
```

---

<a name="quick-start"></a>
<p align="left" width="100%">
  <img src="https://raw.githubusercontent.com/modestimpala/VEmu/refs/heads/main/media/quick%20start.png">
</p>

1. **Install the mod** through r2modmanager.

2. **Launch VotV once** so the mod creates `%LOCALAPPDATA%\VEmu\` and its subfolders. Paste `%LOCALAPPDATA%\VEmu` into Explorer's address bar to open it. All ROMs / cores / BIOS / saves live here. 

3. **Drop a core DLL into `%LOCALAPPDATA%\VEmu\cores\`.** Cores are emulator backends. Grab them from the libretro buildbot:
   > https://buildbot.libretro.com/nightly/windows/x86_64/latest/

   For example, drop `snes9x_libretro.dll` to play SNES games.

4. **Drop a ROM under `%LOCALAPPDATA%\VEmu\roms\`.** Just put `super_mario_world.sfc` directly in `roms\` and the mod figures out the system from the extension. (For zips and more advanced layouts, see [ROMs](#roms).)

5. *(Optional)* **If the core needs a BIOS, drop it into `%LOCALAPPDATA%\VEmu\system\`.** Check `system\required_bios.txt` after the first launch to see what's needed. 

6. **Launch VotV.**:
    - Props are located under the Store -> Essentials -> Electronics
    - Purchase the **GameToy** (handheld) **SGES home console**, or **PlayStation** from the store.
    - Purchase the **Cartridge Dispenser**.
    - Choose your ROM from the dispenser. It dispenses a physical cartridge.
    - Insert the cartridge into the console. For the SGES, plug the AV cord into a TV.
    - **Controller recommended.** Xbox, PlayStation, Switch and generic USB pads all work out of the box. Plug in more for local multiplayer.

### Basic controls (once playing)

- **LEFT click** while holding the device to "gate" your input to the emulator. Without this, keyboard keys drive your character too. Gamepads work without gating.
- **RIGHT click + drag** on the GameToy or Console Controllers to rotate it in your hands. Hold SHIFT to translate sideways, ALT to translate forward/back. (press ALT after RIGHT click)
- **F5/F6** to quicksave/quickload. **Tab** to fast-forward. **F8** to reset the core. Full hotkey list in [Controls](#controls).

That's enough to play. The rest of this README covers customization, ROM layouts, save data, settings, and troubleshooting.

## Do you know what RHI mode you're on? It matters for this mod! 

<p align="center" width="20%">

<img src="https://raw.githubusercontent.com/modestimpala/VEmu/refs/heads/main/media/rhi.png">

</p>

Set this in **Settings → Video → Advanced → RHI Mode**, then restart.

RHI Modes:
- 0 (D3D11) : Fully supported end-to-end 
- 1 (D3D12) : Fully supported end-to-end (recommended)
- 2 (Vulkan) : **Not supported - no video for any core.** UE4 4.27's Vulkan RHI can't import the mod's shared GPU texture, so the screen stays black (audio still plays). If you're on Vulkan, set RHI Mode to **0** or **1** and restart. (A CPU-upload fallback for Vulkan is a possible future addition.)


---

<a name="notes"></a>
<p align="left" width="100%">
  <img src="https://raw.githubusercontent.com/modestimpala/VEmu/refs/heads/main/media/notes.png">
</p>

This is, as far as I'm concerned, a near-feature-complete Libretro frontend baked into VotV. Almost any core runs, it has full gamepad support, save states, fast forward, and more. 

- Controllers: Xbox, PlayStation, Switch and generic USB pads work out of the box (read through SDL, no DS4Windows needed). Every connected controller is a player.
- If one controller shows up as two players, a remapper (DS4Windows etc.) is doubling it - close it or see the link above.

Right now every system works on any kind of cartridge/system prop (there's only two currently.)

I've put a lot of work into making sure this mod works seamlessly with VotV's systems, doesn't introduce lag or input latency, and supports a wide variety of cores. That being said, this mod is easily the most architecturally and technically complex mod I've ever released. There may be issues, odd bugs, potential crashes, and other weirdness.

Included in this Readme are the cores I've personally tested, but I haven't tested every single one, and I have only my specific hardware (Intel CPU, NVIDIA GPU) - Please report any issues you may encounter on GitHub or Discord.

Code in this mod is either written by me or used under permissive open-source licenses (MIT for libretro headers, miniz, and bundled .info files). Non-code assets are my own work or used with credit under their respective licenses (CC BY, etc). **No ROMs, BIOS files, or commercial game content are bundled.**

<a name="file-structure"></a>
<p align="left" width="100%">
  <img src="https://raw.githubusercontent.com/modestimpala/VEmu/refs/heads/main/media/file%20structure.png">
</p>

### 1. Mod folder 

`C:\Users\<user>\AppData\Roaming\r2modmanPlus-local\VotV\profiles\<profile>\shimloader\mod\Moddy-VEmu\dlls\`

```
├── main.dll                       <- the mod itself
├── libretrocpp_corehost.exe       <- the per-core child process host
├── settings.ini                   <- auto-generated on first run; resets on each update
├── cores\info\                    <- shipped .info metadata files 
└── keymaps\_reference.txt         <- shipped reference doc for the keymap format
```

### 2. User data folder 

`%LOCALAPPDATA%\VEmu\` - paste that into Explorer's address bar.

```
├── cores\                <- drop your core DLLs here
│   └── info\             <- (optional) drop newer .info files here to override shipped ones
├── roms\                 <- drop your ROMs here (see ROMs section for layouts)
│   └── <system>\         <- one auto-created per installed core (snes/, nes/, nintendo_64/, ...)
├── system\               <- drop BIOS files here (only if a core needs one)
│   └── REQUIRED_BIOS.txt <- auto-generated each scan; lists what's needed / present
├── saves\                <- SRAM, save states, and core options (auto-created)
│   ├── <system>\         <- per-system subdir: <rom_id>.srm, .state<N>, .state<N>.png, .opt
│   ├── <core>.opt        <- per-core libretro option overrides
│   ├── resume\          <- consoles' running games, saved with your VotV saves (auto-managed)
│   ├── cheats\          <- which cheats you turned on, per game
│   ├── .procedural_covers\  <- auto-generated cover art cache
│   └── corrupted\        <- corrupted ROMs land here
├── keymaps\              <- per-system keybind INIs (auto-generated on first cart load - edit freely)
│   ├── _global.ini       <- frontend hotkey bindings (auto-generated, edit freely)
│   └── _descriptors\     <- auto-generated per-cart input descriptors (reference only)
├── cheats\              <- RetroArch .cht cheat files for the quick menu's Cheats page
├── controllers.ini      <- which controller is which player (auto-written)
├── music\               <- drop .xm / .mod tracker tunes here; play in the Everdrive ROM browser
├── everdrive\           <- optional Everdrive scene extras: fonts\*.png, scroll.txt, greets.txt
└── .core_cache\          <- per-instance core copies (auto-managed)
```

`roms\` will appear (along with one `<system>/` subfolder per installed core) after the first time the mod loads.

#### Putting the user data folder somewhere else

Don't want it on your C: drive? Point VEmu at any folder by setting `user_data_dir` under `[Paths]` in `settings.ini`:

```ini
[Paths]
user_data_dir = D:\Games\VEmu
# environment variables work too:
# user_data_dir = %USERPROFILE%\Documents\VEmu
```

The path is taken **literally** - whatever you name becomes the root that holds `cores\`, `roms\`, `saves\`, etc. (no `\VEmu` is appended for you). A relative path is resolved against the mod folder. The folder is created if it doesn't exist.

Two things to know:
- **It only applies at game launch.** Unlike most settings (which re-apply on cart eject/reinsert), the data root is locked in once at startup. It requires a VotV restart. 
- **Move your data first.** VEmu doesn't migrate anything. Before launching with a new `user_data_dir`, copy your existing `%LOCALAPPDATA%\VEmu\` contents into the new folder.

---

<a name="cores"></a>
<p align="left" width="100%">
  <img src="https://raw.githubusercontent.com/modestimpala/VEmu/refs/heads/main/media/cores.png">
</p>

**No cores are bundled** - you must supply your own. Matching `.info` files **are** bundled (metadata that tells the mod what each core supports).

### Adding a core

1. Grab the core DLL from the libretro buildbot:

   > https://buildbot.libretro.com/nightly/windows/x86_64/latest/

   > (Or download them all: https://buildbot.libretro.com/nightly/windows/x86_64/RetroArch_cores.7z)

2. Drop the `.dll` into `%LOCALAPPDATA%\VEmu\cores\`.

For the full list of available cores and what systems they emulate, see the libretro core list:

> https://docs.libretro.com/guides/core-list/


### Connecting a console to a TV

Use the AV cord on the back of the console. The mod connects to vanilla TV props. (Not SmartTV - ironic, I know. Coming soon?) Make sure the TV is set to a channel, not the default "invalid channel". 

### Light gun

The **Zapper** plugs into a console's controller port like a controller. Hold it, point it at the TV the console is connected to, and **left click** to fire. There's no on-screen crosshair; you aim with the gun itself. Supported on NES (Duck Hunt and friends), PlayStation (GunCon games like Time Crisis), Saturn (Virtua Gun games like House of the Dead, on the default Beetle Saturn core) and Dreamcast (Flycast).

- Some cores draw their own crosshair; turn it off in the quick menu's Options if you want it gone (`fceumm_show_crosshair`, Beetle PSX "gun cursor", Beetle Saturn "virtuagun crosshair", Flycast "lightgun1 crosshair").
- The gun's other buttons are on keys VotV leaves free: `Enter` Start, `Y` Select, `G` / `B` / `I` A / B / C, `N` reload, `U` `J` `H` `K` d-pad. Rebind them in `_global.ini` (`Gun_*`) or F9 > Controls. A controller's buttons work too.
- Firing off the screen reloads, as on the real guns.

### Limits

Most cores that use a standard gamepad should work. Cores that need unusual input are currently **not supported** or work only partly:

- **Motion/pointer controllers:** games that need a real Bluetooth Wii Remote. Wii pointer aiming works on a stick, or with your controller's gyro (see [Motion controls](#motion-controls)).
- **Touchscreen input:** for example, Nintendo DS games that depend on the touchscreen or a stylus.
- **Keyboard- or mouse-only cores:** for example, DOSBox and other computer emulators that need a full keyboard.

### Personally tested

I've confirmed these work. Anything *not* on this list isn't unsupported, it just hasn't been verified by me. Please report results either way.

| System | Core DLL |
|---|---|
| SNES | `snes9x_libretro.dll` |
| NES | `fceumm_libretro.dll` |
| GB/GBC/GBA | `gambatte_libretro.dll`, `mgba_libretro.dll` |
| N64 | `mupen64plus_next_libretro.dll` (gLideN64 OpenGL) |
| PSX | `pcsx_rearmed_libretro.dll`, `mednafen_psx_hw_libretro.dll` (Beetle PSX HW) |
| PS2 | `pcsx2_libretro.dll` (LRPS2) |
| PSP | `ppsspp_libretro.dll` |
| Dolphin | `dolphin_libretro.dll` |

---

<a name="bios-files"></a>
<p align="left" width="100%">
  <img src="https://raw.githubusercontent.com/modestimpala/VEmu/refs/heads/main/media/bios%20files.png">
</p>

Some emulator cores need a **BIOS file** (the firmware from the original console) to run games. These go in `%LOCALAPPDATA%\VEmu\system\`.

### Do I need one?

It depends on the core. Each libretro core has its own page in the libretro docs that lists exactly which BIOS files it needs, which are optional, and what the expected filenames + checksums are.

> https://docs.libretro.com/library/bios/  (pick your core, it will jump to BIOs section)

Example: PCSX-ReARMed's BIOS list lives at https://docs.libretro.com/library/pcsx_rearmed/#bios.

### `system/required_bios.txt` (auto-generated)

Every time the mod scans the manifest, it writes a fresh `required_bios.txt` into `system/` summarising what each installed core wants and whether the file is currently present. It's the fastest way to see what's missing.

```
## pcsx_rearmed_libretro.dll  (PCSX-ReARMed)
    [X] scph5500.bin                  optional  -- scph5500.bin (PS1 JP BIOS)
    [X] scph5501.bin                  optional  -- scph5501.bin (PS1 US BIOS)
    [X] scph5502.bin                  optional  -- scph5502.bin (PS1 EU BIOS)
    [ ] psxonpsp660.bin               optional  -- psponpsx660.bin (PSP PSX Emu BIOS)
```

`[X]` = present, `[ ]` = missing. `REQUIRED` means the core won't run games without it; `optional` means it improves accuracy or boot logos but isn't load-blocking. The file is regenerated on every scan (don't edit).

### How to add a BIOS

1. **Legally acquire the file.** VEmu will never ship any BIOS files.
2. **Use the exact filename** the core expects. Filenames are case-sensitive on some systems and the core won't search for variants. Either copy the name straight out of `required_bios.txt`, or check the core's libretro docs page.
3. **Drop it directly into `%LOCALAPPDATA%\VEmu\system\`** - no subfolders (unless the core specifies one, e.g. `Mupen64plus/IPL.n64`).
4. **Restart the game.** Cores read the BIOS once at load time. Requires full reload.

---

<a name="roms"></a>
<p align="left" width="100%">
  <img src="https://raw.githubusercontent.com/modestimpala/VEmu/refs/heads/main/media/roms.png">
</p>

ZIP and 7z archives are supported. Arcade cores (FBNeo, MAME) get the romset archive directly without extracting.

It's recommended your ROM file or folder names follow the "No-Intro" naming convention, i.e. `Donkey Kong Country (USA, Europe) (En,Fr,De,Es,It).zip` for Thumbnail images to resolve properly. 

Three layouts work, and you can mix them:

### Layout 1 - loose ROMs at the root

```
roms\
├── pokemon_red.gb
├── super_mario_bros.nes
└── super_mario_world.sfc
```

**Do not place loose zips or 7z files in `roms\`. Archives must go in system-specific ROM directories.**

System inferred from extension. Cover art beside the ROM (`pokemon_red.png`) is picked up automatically.

### Layout 2 - system folders

```
roms\
├── snes\
│   ├── super_mario_world.sfc
│   └── chrono_trigger.zip
├── nes\
│   └── zelda.nes
└── n64\
    └── mario_64.z64
```

`.zip` / `.7z` files only work inside a system folder, or with a `core.txt` override (since the extension alone doesn't tell us which core to use).

Recognized folder names:

- **Short aliases (5)**: `snes`, `nes`, `gb`, `gbc`, `gba` - friendly shortcuts that map to the libretro database name.
- **Anything else**: the `systemid` from a core's `.info` file - e.g. `nintendo_64`, `playstation`, `playstation_portable`, `nintendo_gamecube`, `nintendo_ds`, `sega_genesis`. Check the systemid line in the mod folder's `cores\info\<core>_libretro.info` (shipped metadata) if you're unsure.

**You don't have to create these yourself.** On every scan, the mod auto-creates an empty `roms/<system>/` for each installed core (alias name where one exists, otherwise the systemid). So dropping `snes9x_libretro.dll` into `cores/` and re-launching is enough to make `roms/snes/` appear.

### Layout 3 - one folder per ROM

```
roms\
└── snes\
    └── super_mario_world\
        ├── super_mario_world.sfc
        ├── cart.png         <- cover art (optional)
        └── core.txt         <- per-ROM core override (optional)
```

Use this layout if you:
 - Have multi-file disc images
 - Want a custom cover, a custom display name, or to override which core runs the game. 
 
 The folder name becomes the cart's display name (underscores become spaces).

### Cover art

Put `cart.png` (or `cover.png`, `box.png`, `art.png`) in the cart folder. For loose ROMs, name it after the ROM stem (`pokemon_red.png`).

If you don't provide one, the mod tries to grab a cover from [libretro-thumbnails](https://thumbnails.libretro.com) on first cart spawn:

- **Folder layout**: image lands at `<cart-folder>\cart_auto.png` (your `cart.png` is never touched - manual covers always win).
- **Loose ROMs**: image lands at `<rom-stem>.png` next to the ROM. If you want to keep a manual one, place it first.

### Disc / CD case games

You can choose to spawn disc-based systems (PSX, PS2, PSP, GameCube/Wii, etc.) as a **jewel / CD case** holding one or more **disc** props instead of a cartridge. You can do this for normal cartridge games too. Disc games are cartridges to the loader, so the same cover rules apply. Put `cart.png` (or `cover.png`, `box.png`, `art.png`) in the game's folder, or let the mod fetch a cover automatically from libretro-thumbnails.

The case and the disc each have their own art:

| Surface | Your file (folder layout / loose ROM) | If you don't provide one |
|---|---|---|
| **Case front** | `cart.png` (or `cover` / `box` / `art`) / `<stem>.png` | Boxart from libretro-thumbnails (`cart_auto.png` / `<stem>.png`), else a generated PlayStation-style front with the title and system name |
| **Case back** | `back.png` / `<stem>_back.png` | Composed from the libretro title screen + gameplay snap (`title_auto.png`, `snap_auto.png` / `<stem>.title.png`, `<stem>.snap.png`), else the stock jewel-case back |
| **Disc face** | `disc1.png`, `disc2.png`, ... then `disc.png` / `<stem>_disc.png` | Single disc: the front art. Multi-disc: a generated "DISC n OF N" label drawn over the boxart |

`.jpg` works for all of the above, but generated/composited art (back, disc label) only blends `.png` sources. The case downloads its missing art one file at a time, so the back and disc label fill in a few seconds after the first spawn. Failed downloads leave a `.failed` marker so they aren't retried every launch; delete it to retry.

#### Multi-file and multi-disc games

- **Multi-file disc images** (`.cue` + `.bin`, multi-track dumps): use [Layout 3](#layout-3---one-folder-per-rom) so every file stays together in one folder. Point the core at the `.cue`.
- **Multi-disc games**: put every disc in the game's folder, as long as the core accepts `.m3u`. The mod finds them in one of two ways:
  - an `.m3u` playlist already in the folder (the first alphabetically is used; `#` comments and `|label` suffixes are ignored), or
  - two or more images of the same format. The mod writes `<game>.m3u` for you, in natural order (`Disc 2` before `Disc 10`). Format preference: `cue > chd > pbp > ccd > toc > mds > cdi > gdi > iso > cso > img > bin`.

  The generated `.m3u` is never rewritten, so **delete it after adding or removing a disc**.
- The save / memory card is shared by every disc of a game.

#### Handling discs in game

- Each disc is its own prop, and the case remembers which discs are inside. 
- You can live-swap game discs for multi-disc games. 
- **Removing a disc** from a running multi-disc game opens the tray and the game keeps running, so you can put in the next disc when it asks ("insert disc 2").
- You can also swap discs from the **F9** quick menu (Disc page).

### Per-ROM core override

Drop a `core.txt` file into the cart folder containing one line - the core DLL filename:

```
snes9x2010_libretro.dll
```

This wins over the system default. Useful if you want a different core for one specific game (or to use a core whose `.info` file you don't have).

### 3DS game updates and DLC (Citra)

The Citra core can't install `.cia` files itself. Install updates/DLC once with standalone Citra or [Azahar](https://azahar-emu.org/), then copy them into VEmu's copy of the 3DS SD card. After that the core applies them automatically.

1. **Boot the game once in VEmu.** This makes the core create its data folder under `saves\` (`%LOCALAPPDATA%\VEmu\saves\Citra\` for `citra_libretro.dll`).
2. **Install the `.cia` files in the standalone emulator** (File -> Install CIA...).
3. **Open the standalone emulator's SD folder**, usually `%APPDATA%\Azahar\sdmc\` or `%APPDATA%\Citra\sdmc\`, and go to:
   ```
   sdmc\Nintendo 3DS\00000000000000000000000000000000\00000000000000000000000000000000\title\
   ```
4. **Copy these two folders** into the same path under VEmu's `saves\Citra\sdmc\` (create the folders if they're missing, merge if they exist):
   - `0004000e\` - game updates
   - `0004008c\` - DLC

   **Don't copy `00040000\`** - that's where game saves live, and it would overwrite your VEmu saves with the standalone ones.
5. **Reinsert the cartridge.**

Notes:
- Don't put update/DLC `.cia` files in `roms\` - they'll show up as cartridges that won't boot.
- Base games must be decrypted `.3ds` / `.cci` / `.cxi` files. `.cia` games can't be loaded directly by the libretro core.
- If the game ignores the update, the installed files are probably still encrypted. Try installing a decrypted `.cia` instead.

---

<a name="playing-in-game"></a>
<p align="left" width="100%">
  <img src="https://raw.githubusercontent.com/modestimpala/VEmu/refs/heads/main/media/playing%20in%20game.png">
</p>


Props are located under the Store -> Essentials -> Electronics.

- **GameToy - Handheld** - Hold-and-play, has its own screen.
- **SGES - Home console** - Super Gaming Entertainment System. Needs a TV. Plug in with the included AV cord; the screen output appears on the TV. 
- **PlayStation - Home console** - Disc based system. 
    - **Console Controllers** are also included in the store and are needed to control consoles. 
- **Cartridge dispenser** - A prop that lists every ROM and allows you to spawn them as cartridges. Costs points per cartridge.

### VEmu Everdrive (in-game ROM browser cartridge)

The dispenser also lists a **VEmu Everdrive** cartridge. Instead of being one game, it's a flash-cart: insert it into the GameToy or SGES and an on-screen ROM browser appears *on the device's own screen* - no separate window, rendered right through the same video path as the games.

- **Browse** with the D-pad / arrow keys: ◄ ► switches between system columns (SNES, NES, N64, PSX...), ▲ ▼ moves through that system's ROM list.
- **Type to search** - start typing and the list filters across *all* systems (live, as-you-type); **B** clears the filter.
- **A launches** the highlighted ROM - it loads exactly as if you'd inserted that game's own cartridge, while the Everdrive stays in the slot.
- **Return to the browser** any time from in-game with **F7** (rebind `Frontend_OpenMenu` in `_global.ini`; a gamepad button works too).

Same input rules as playing: **keyboard** navigation needs you to "gate" the device first (LEFT click while holding), **gamepad** navigation works without gating.

#### Background music (optional)

Drop `.xm` (FastTracker II) or `.mod` (ProTracker / Amiga, including `mod.name` style file names) tracker modules - keygen and cracktro chiptunes - into `%LOCALAPPDATA%\VEmu\music\`. While the Everdrive browser is open they play shuffled, looping the folder, out of the device's speaker (3D-attenuated, at your master volume). No music = silent browser. VEmu ships **no** music. 

#### Intro, demo and keygen scenes

The Everdrive puts on a bit of a show, oldskool cracktro style:

- **Intro** - inserting the cart plays a cracktro: copper bars, a wobbling chrome logo, your library stats typed out, and a sine scroller over a rippling mirror. Any button skips to the browser. Coming back from a game with **F7** skips it.
- **Keygen** - picking a ROM pops a keygen window for a moment (serial, progress bar, the works) before the game boots. Any button skips it.
- **Demo screensaver** - leave the browser idle and a demo takes over, cycling plasma, a burning logo, a tunnel with greetings, a rotozoomer, a checkerboard floor with a dot ball, and a warp starfield, with a scroller touring your library. Any input wakes it.

All three can be turned off, or the idle time changed, from the browser's settings panel (**Start**) or under `[Frontend]` in `settings.ini` (`everdrive_intro`, `everdrive_launch_fx`, `everdrive_saver_sec`). Changes apply the next time the Everdrive opens.

Make it yours in `%LOCALAPPDATA%\VEmu\everdrive\`:

- `fonts\*.png` - bitmap scroller fonts. One is picked at random each time the browser opens; without any, a built-in chrome font is used. The classic layout loads as-is: square cells ten to a row, starting at space in ASCII order (`!"#$%&'()*+,-./0-9:;<=>?@A-Z`), on a solid background colour, which is what most of the old DOS/Amiga scroller font sheets (e.g. the [f0ntbin](https://github.com/phracker/f0ntbin) collection) use. For any other layout put a `.txt` with the same name next to it:
  ```
  cell=16x16
  chars=ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789!?.,:-
  blank=,
  key=000000
  ```
  `cell` is the glyph cell size, `chars` the glyphs in order (left to right, top to bottom), `blank` any cells holding a watermark rather than a letter, and `key` the background colour (the most common colour in the image if left out). A font that's missing most letters is skipped; `UE4SS.log` says why.
- `scroll.txt` - your own intro scroll text. `{ROMS}` and `{SYSTEMS}` become your library counts.
- `greets.txt` - one greeting per line for the demo's tunnel part.

<a name="corruptions"></a>
<p align="left" width="100%">
  <img src="https://raw.githubusercontent.com/modestimpala/VEmu/refs/heads/main/media/corruptions.png">
</p>

> **[SPOILERS]** - Click below to expand if you want the full mechanic explained.
<details>
<summary>Click to reveal corruption mechanic</summary>
You can microwave cartridges to corrupt them. This is exactly like the corruption tools you might find online, but randomly done on the cartridge's ROM behind the scenes. It only does it once on the first zap. If you take it out, hold it, put it in your inventory, etc, it will reset and allow you to microwave it again. You can technically re-corrupt the already corrupted ROM. 

The corruption is actually deterministic - it gives it a seed, and writes the corrupted ROM to `saves\corrupted\` with a filename that includes the original ROM ID and the microwave seed. The original ROM is left untouched in `roms\`.

- Corrupted ROMs are written to `saves\corrupted\<rom_id>_<seed>.<ext>`. Originals are never modified.
- Per-system protection attempts to keep the game playable
- Each microwave session uses a fresh random seed, baked into the filename. Same seed + same corruption, so you can save an interesting one for later.

**"Un-corrupting" can be done by dunking it in water.**

**Warning**: these ROMs can be very unstable. HW cores like mupen64plus_next, psx_rearmed, and dolphin are more likely to crash horribly. Simple software cores like snes9x and gambatte are safer for this. 
</details>

<a name="controls"></a>
<p align="left" width="100%">
  <img src="https://raw.githubusercontent.com/modestimpala/VEmu/refs/heads/main/media/controls.png">
</p>

Some default keymaps live in `keymaps\<system>.ini`. They ship pre-configured for keyboard + Xbox-style gamepad. Changes take effect on the next cart insert.

### Keyboard - cart-era systems (NES, SNES, GB/GBC, GBA, and other d-pad systems)

Matches RetroArch's default Player 1 keyboard layout. The same layout is the default for other d-pad systems: Master System, PC Engine, PC-FX, Saturn, Nintendo DS, Neo Geo Pocket, WonderSwan, Atari 2600/7800/Lynx, 3DO, Pokemon Mini, Supervision, Mega Duck, Vectrex, arcade (FBNeo / MAME / Neo Geo), and fantasy consoles (PICO-8, TIC-80, WASM-4, ...). Those also get `1` / `2` for L2 / R2. On arcade, Select (`RightShift`) inserts a coin.

| Key          | Action                |
|--------------|-----------------------|
| `↑ ↓ <- →`    | D-Pad                 |
| `Z` / `X`    | B / A                 |
| `A` / `S`    | Y / X  *(SNES only)*  |
| `Q` / `W`    | L / R  *(SNES, GBA)*  |
| `Enter`      | Start                 |
| `RightShift` | Select                |

### Keyboard - Mega Drive / Genesis

Laid out like the pad: the A/B/C row on `Z X C`, the 6-button X/Y/Z row right above it on `A S D`.

| Key          | Action        |
|--------------|---------------|
| `↑ ↓ <- →`    | D-Pad         |
| `Z` `X` `C`  | A / B / C     |
| `A` `S` `D`  | X / Y / Z     |
| `Enter`      | Start         |
| `RightShift` | Mode          |

Master System / Game Gear games running on Genesis Plus GX use `X` (button 1) and `C` (button 2).

### Keyboard - stick-driven systems (N64, PSX/PS2, PSP)

D-pad on arrow keys, **WASD drives the left analog stick** (so games that switch to analog mode work on keyboard).

| Key          | Action                                     |
|--------------|--------------------------------------------|
| `↑ ↓ <- →`    | D-Pad                                      |
| `W A S D`    | Left analog stick (full deflection)        |
| `Z` / `X`    | B / A    *(N64: A/B • PSX/PSP: Cross/Circle)* |
| `C` / `V`    | Y / X    *(PSX/PS2/PSP: Square/Triangle)*  |
| `I J K L`    | C-Up / C-Left / C-Down / C-Right *(N64)*   |
| `Q` / `E`    | L / R    *(L1/R1 on PSX)*                  |
| `LeftShift`  | Z trigger *(N64)*                          |
| `1 2 3 4`    | L2 / R2 / L3 / R3 *(PSX/PS2)*              |
| `Enter`      | Start                                      |
| `RightShift` | Select *(PSX/PS2/PSP)*                     |

### Keyboard - DOOM (PrBoom)

FPS-style layout. WASD is split: W/S move forward/back via D-pad, A/D strafe via libretro L/R (PrBoom's "Strafe Left/Right"), and the arrow keys turn the camera. 

| Key           | Action                            |
|---------------|-----------------------------------|
| `W` / `S`     | Move forward / back               |
| `A` / `D`     | Strafe left / right *(L / R)*     |
| `<-` / `→`     | Turn left / right *(D-pad)*       |
| `LeftCtrl`    | Fire *(A)*                        |
| `Space`       | Use *(B)*                         |
| `LeftShift`   | Run, hold *(Y)*                   |
| `LeftAlt`     | Strafe modifier, hold *(X)*       |
| `Z` / `X`     | Previous / next weapon *(L2/R2)*  |
| `Enter`       | Menu *(Start)*                    |
| `M`           | Map *(Select)*                    |

If you switch PrBoom's User 1 device type to **Gamepad Modern** in core options, the analog sticks should drive strafe + look automatically (already bound on the gamepad side).

**Regenerating a keymap file.** The mod writes `keymaps\<system>.ini` once on first cart load and never touches it again. Delete the file and re-launch to re-generate.

### Frontend hotkeys (any cart, any system)

These come from `keymaps\_global.ini`:

| Key         | Action               |
|-------------|----------------------|
| `F5`        | Quick save (slot 0)  |
| `F6`        | Quick load (slot 0)  |
| `F1` / `F2` | Save / load slot 1   |
| `F3` / `F4` | Save / load slot 2   |
| `F8`        | Reset core           |
| `F9`        | Quick menu (pause, save/load slots, core options, cheats, audio filter, disc, controllers, controls, settings) |
| `F10`       | Toggle FPS overlay   |
| `Pause`     | Pause / resume       |
| `Tab`       | Fast-forward (hold) - default 4x  |
| `R`         | Rewind (hold)        |
| `Backspace` | Frame advance        |
| `F7`        | Open VEmu Everdrive browser (for carts launched from it) |

**Quick menu controls** (the cart's own buttons): up/down to move, A to select or change, left/right to cycle a value or the save slot, B to go back (or resume from the top page), L/R to jump between option sections, X to restore an option's default. Save/Load State shows the slot's screenshot and save time when the screen has room.

Save state slots 0-9 are supported (`Frontend_SaveState_<N>` / `Frontend_LoadState_<N>`); only a few are bound by default - bind the rest in `_global.ini` if you want them.

Rewind keeps a compressed history of recent savestates in memory (128 MB per cart by default - minutes of history for SNES-era systems). Tune it with `rewind_enabled` / `rewind_buffer_mb` / `rewind_granularity` under `[Frontend]` in `settings.ini`. Cores whose savestates are too slow or too large to take every frame (PCSX2, Dolphin, ...) switch rewind off for themselves, and pressing `R` tells you so.

The FPS overlay toggle (`Frontend_ToggleFps`) is runtime-only - it flips the overlay on/off this session but doesn't persist to `settings.ini`. To make it permanent, edit `[Debug] fps_overlay` in `settings.ini`.

The overlay shows the measured emulation rate (it drops below the game's rate when the core can't keep up). While it's on, a `perf:` line is written to `UE4SS.log` every 5 seconds: loop rate vs. target, core and shipped frames per second, per-frame work time (average / max vs. the frame budget), late frames, and for Vulkan cores the time spent waiting on the GPU copy.

**Gamepad bindings work here too.** The defaults above are keyboard for convenience, but any `Frontend_*` action accepts a gamepad button on the LHS - add a line like `Gamepad_FaceButton_Top = Frontend_Pause` (Y button on Xbox) to `_global.ini` and you can pause / quicksave / fast-forward with the controller alone (no need to gate via LEFT click). Gamepad-bound frontend hotkeys dispatch even when the device isn't currently focused, same as gamepad cart inputs.

### Keyboard vs gamepad gating

- **Keyboard** keys feed the emu only while you're actively "using" the device (LEFT click while holding either GameToy or SGES Controller). This stops `W` from driving both your character and the d-pad.
- **Gamepad** buttons (anything starting with `Gamepad_`) always feed the emu while you hold the device (or a home console's controller), gated or not. So you can game / pause / quicksave with a controller without focusing the device.

### Multiple controllers

Every connected controller is a player, in connection order: player 2's pad drives controller port 2 with the same layout as player 1. Each controller is remembered in `controllers.ini` (user data folder) and gets its player number back on reconnect. The keyboard and gamepad hotkeys belong to player 1. Settings live under `[Input]` in `settings.ini` (`gamepad_backend = ue` restores the old one-Xbox-pad behaviour). 

<a name="motion-controls"></a>
### Motion controls

With a gyro controller (DualSense, DualShock 4, Switch Pro, ...) on the default SDL backend:

- **Games that read motion** get it directly: GBA tilt carts in mGBA, the Wii Remote in Dolphin.
- **Tilt and shake as buttons.** In F9 > Controls, while a row is waiting for an input, tilt the controller (left, right, forward or back, past about 20 degrees) or shake it. On a stick row, tilting steers that stick on top of the real one.
- **Gyro aim.** F9 > Controls > Gyro aim turns the controller into a pointer on the left or right stick, for Wii pointer games and light gun games.
- **Held controller moves.** `[Input] controller_motion = true` in `settings.ini` makes the controller in your character's hands tilt and jolt along with your real one.

Turn all of it off with `[Input] motion = false`.

### Customizing keybinds

The quick menu's **Controls** page (F9) is the easy way: pick what to edit (this game, all games on the system, or hotkeys), controller or keyboard, and which player, then press the new button. It writes the same files described here.

Keybinds live in **per-system `.ini` files under `keymaps\`**. You don't have to create these yourself: the mod auto-writes `keymaps\<system>.ini` (and `_global.ini`) the first time you insert a cart for that system, seeded from the compiled defaults. Changes take effect on the next cart insert.

```
keymaps\
├── _global.ini       <- frontend hotkeys (pause, save state, etc.)
├── _reference.txt    <- full list of valid key names and actions
├── _descriptors\     <- auto-generated per-cart input descriptors (read-only reference)
├── snes.ini          <- appears after first SNES cart insert
├── nes.ini           <- appears after first NES cart insert
├── gb.ini
├── gba.ini
└── n64.ini
```

Format is `<UE-key-name> = <action>`. Key names are UE FKey FNames - so `RightShift`, not `Right Shift` - `Tab`, `BackSpace`, `Gamepad_FaceButton_Bottom`, etc. See `_reference.txt` for the complete bindable-key list and actions. Empty right-hand side unbinds.

### How to layer keybinds

Load order, top-to-bottom: First loaded, last loaded. Last loaded wins. 

For a SNES ROM file called `Super Mario World`:

| Cart input | Frontend hotkeys |
|---|---|
| compiled defaults | (none) |
| `snes.ini` | `_global.ini` |
| `snes.super_mario_world.ini` | `_global.snes.ini` |
|   | `_global.snes.super_mario_world.ini` |


`<rom>` matches the rom_id used in `roms/<system>/<rom>.srm` and `_descriptors/<system>.<rom>.txt` - copy from there to avoid typos.

**Corrupted carts inherit regular bindings.** A corrupted cart's customized keymap would need a seed suffix (`banjo-tooie (usa)_1815209044.ini`). The regular file loads first, then the seed-specific one on top. 

### Shipped per-game layouts

Some games ship with a per-cart layout. VEmu writes it as `keymaps\<system>.<rom>.ini` on first load, and never rewrites it.

- **GoldenEye 007** (N64): twin-stick, with your pad playing both N64 controllers. Left stick moves and strafes (analog), right stick looks and turns, RT fires, LT aims. **Set the in-game Control Style to 2.2 Galore.** 

Bindings can target another controller port with a `P2:` .. `P4:` prefix (`Gamepad_LeftTrigger = P2:L2`); see `_reference.txt`.

### `keymaps\_descriptors\` (auto-generated)

ROM-specific keybind information returned by cores:

<details>
<summary>Click to read about keymap descriptors</summary>
The first time any cart loads, the running core reports its **input descriptors** via libretro's `RETRO_ENVIRONMENT_SET_INPUT_DESCRIPTORS` callback - basically "for this game, the A button means X, the L trigger means Y". The mod captures that and writes it to `keymaps\_descriptors\<system>.<rom>.txt` as a read-only reference. The runtime does **not** parse these files; they exist purely so you can see what each RetroPad button actually does in a specific game before you bind a real key to it.

Example (Banjo-Tooie, N64):

```
[port 0]
B            -- "A Button (C3)"
Y            -- "B Button (C2)"
A            -- "(C1)"
X            -- "(C4)"
R2           -- "C Buttons Mode"
L2           -- "Z Trigger"
...
```

If a button or axis is missing from this file, the core didn't advertise it (usually means the game doesn't use it). Use the action tokens here (`B`, `Y`, `L2`, `Stick_L_X`, etc.) as the RHS values when writing a per-cart override like `keymaps\n64.banjo-tooie (usa).ini`.
</details>

### Controller device type (`[devices]`)

Some cores emulate more than one kind of controller per port and only hook up the right one when the frontend asks for it. The headline case is **Dolphin**: a Wii game that needs the **Nunchuk** gets a bare Wii Remote (no stick, no C/Z buttons) unless you explicitly select the Wiimote + Nunchuk type. Without this, nunchuk-required games are unplayable even though the core "runs".

Add a `[devices]` section to a keymap file. It layers exactly like the keybind sections - `<system>.ini` sets a per-core default, `<system>.<rom>.ini` overrides it per game. Keys are `port0`..`port3` (`port` alone means `port0`); only the ports you name change.

```ini
[devices]
port0 = nunchuk        ; attach Wii Remote + Nunchuk on port 0
```

The value is a friendly alias **or** a raw libretro device id (decimal or `0xHEX`). The aliases are Dolphin's Wii/GC types; the numeric form works for **any** core.

| alias | id | meaning |
|---|---|---|
| `joypad` / `wiimote` | `0x1` | RetroPad / bare Wii Remote |
| `wiimote_sideways` | `0x201` | Wii Remote held sideways |
| `wiimote_nunchuk` / `nunchuk` | `0x301` | **Wii Remote + Nunchuk** |
| `classic` / `classic_controller` | `0x401` | Classic Controller |
| `classic_pro` | `0x501` | Classic Controller Pro |
| `gamecube` / `gc` | `0x601` | GameCube pad on a Wii title |
| `real_wiimote` | `0x600` | real Bluetooth Wii Remote passthrough |
| `none` | `0x0` | explicitly disconnect the port |

**Finding the right id for a non-Dolphin core:** load the game once and check the corehost log - each port prints what it advertises, e.g. `controller info: port 0 ... id=0x301 -- "WiiMote (Nunchuk)"`. Drop that id (alias or number) into `[devices]`.

**Wiimote pointing (IR):** by default Dolphin maps the IR pointer to the **right analog stick** (`dolphin_ir_mode`), so aiming works on a normal gamepad with no extra setup - C → face X, Z → face Y, Nunchuk stick → left stick. [Gyro aim](#motion-controls) can drive that stick with your controller's gyro. Dolphin's *mouse* IR mode (`dolphin_ir_mode = 2`) and touch-screen input aren't wired yet.

Example file `keymaps\<dolphin_system_tag>.<rom>.ini`:

```ini
[devices]
port0 = nunchuk
```

---

<a name="save-data"></a>
<p align="left" width="100%">
  <img src="https://raw.githubusercontent.com/modestimpala/VEmu/refs/heads/main/media/save%20data.png">
</p>

Everything lives under `%LOCALAPPDATA%\VEmu\saves\<system>\`:

| File | What |
|---|---|
| `<rom_id>.srm` | Battery save (SRAM). Flushed every 30 s while the cart is loaded; tunable via `[SRAM] flush_interval_sec` in `settings.ini`. |
| `<rom_id>.state<N>` | Save state slot `N` (0-9). A toast appears when one is written. |
| `<rom_id>.state<N>.png` | Thumbnail PNG of the framebuffer at the moment of save - written automatically next to the state file. Useful when picking a slot to load. |
| `<rom_id>.opt` | *(optional)* Per-game libretro core options. Overlays whatever's in `%LOCALAPPDATA%\VEmu\saves\<core>.opt`. See [Per-game core options](#per-game-core-options). |

All of these follow you across hold/drop cycles and across game sessions. Pull the cart, save it for later, come back next session, it'll pick up where you left off. To wipe a save: delete the file. To back up: copy the `saves\` folder.

### Resume with your VotV save

Saving Voices of the Void (including quicksaves and autosaves) also saves every console that's running a game. Loading that save puts each console back exactly where it was: same game, same moment, same power and pause state. The Everdrive goes straight back into the game it was running.

- The game boots for a moment with the screen dark before it jumps back, so the console (and a disc drive) has finished starting up. If a game comes back broken, raise **Resume delay** in F9 > Settings (`[State] resume_delay_sec`, default 3 s).
- Snapshots are compressed and kept in `saves\resume\`. Ones no VotV save uses any more are deleted, and `[State] resume_max_mb` (default 4 GB) caps the folder; past it the oldest go, and loading their VotV saves starts the game fresh.
- Turn it off with **Resume on load** in F9 > Settings (`[State] resume_enabled`).
- A snapshot belongs to one core version. After updating a core, a resume may start the game fresh instead.

### Per-game core options

Libretro cores expose their own option grids (renderer, region, internal resolution, etc.) - these are advertised to the frontend at game-load time. VEmu writes the live values to `%LOCALAPPDATA%\VEmu\saves\<core>.opt` whenever the core asks. You can also hand-edit that file.

Changing a core's internal resolution from the quick menu takes effect mid-game, at full sharpness. Hardware-rendered cores (Dolphin, etc.) rebuild their renderer for it, so expect a short pause (about a quarter second) at the switch.

For per-game overrides (e.g. force a specific renderer for one game), use the quick menu: **Options** has a switch at the top for **Every game** / **This game**. In **This game**, changes only apply to the running cart, a dot marks options set for it, **X** puts one back to the every-game value, and **Clear this game's options** drops them all. By hand, drop a file at `%LOCALAPPDATA%\VEmu\saves\<system>\<rom_id>.opt` with the keys you want to override - same `key = value` format. Loaded *on top of* the per-core file, so you only need to list the keys you're changing.

For what keys each core exposes, see that core's libretro docs page under "Core options".

---

<a name="settings"></a>
<p align="left" width="100%">
  <img src="https://raw.githubusercontent.com/modestimpala/VEmu/refs/heads/main/media/settings.png">
</p>

Install-wide preferences live in **`settings.ini`** in the mod folder (next to `main.dll`). This is the "frontend config" tier - like RetroArch's `retroarch.cfg`. r2modman's config UI can read/write it from this location.

### Auto-generated on first run

Neither `settings.ini` nor `settings.example.ini` is included. On first launch, the mod creates `settings.ini` beside `main.dll` if it doesn't already exist.

**Heads up:** `settings.ini` resets on every mod update (because r2modman wipes the mod folder during update). If you've customized it heavily, copy it somewhere safe before clicking Update. Only your *VEmu preferences* live in this file - ROMs / saves / BIOS / keymaps are in `%LOCALAPPDATA%\VEmu\` and survive updates.

Most settings can also be changed in game from the quick menu's **Settings** page (F9), which saves them here. To edit by hand: open `settings.ini`, uncomment the lines you want, edit values, save. Settings added by a mod update are appended to your file automatically.

To start over: delete `settings.ini` and re-launch.

### What's in it

| Section | What it tunes |
|---|---|
| `[Paths]` | `user_data_dir` - relocate the whole user-data folder ([details](#putting-the-user-data-folder-somewhere-else)); `cheats_dir` |
| `[Defaults]` | Fallback `core =` / `rom =` for the cartridge dispenser |
| `[Frontend]` | Message time, fast-forward speed, rewind, Everdrive intro / keygen / screensaver |
| `[State]` | Save state slot range, [resume with your VotV save](#resume-with-your-votv-save) (on/off, disk budget, delay) |
| `[SRAM]` | Battery-save flush cadence (default 30 s) |
| `[Runtime]` | `threaded_core`  |
| `[Audio]` | Sample rate, buffer sizes, master volume, resampler quality, audio effect (`.dsp`) |
| `[Video]` | Graphics API for 3D cores: `auto`, `vulkan`, `d3d11` or `opengl` |
| `[Input]` | SDL or UE controller backend, stick deadzone, ignored controllers, rumble, motion sensors, held-controller motion |
| `[Device]` | Advanced console hand-off timing |
| `[Debug]` | On-screen message baking, FPS overlay, log detail |


`settings.ini` is **global only**. Per-system and per-cart customization lives in the other two config tiers, which DO cascade:

- **Input bindings + frontend hotkeys** -> `keymaps\` (see `keymaps\_reference.txt`). Per-system override files like `snes.super_mario_world.ini` work here.
- **Libretro core options** -> `saves\<core>.opt` and `saves\<system>\<rom>.opt`. Per-core, then per-game overlay.

### Reload behavior

Hand edits to `settings.ini` are read when VotV starts. Changing anything on the quick menu's Settings page also re-reads the file.

Once read, most settings apply straight away or on the next cart insert; the Settings page says which for each row. These need a VotV restart: `user_data_dir`, `threaded_core`, `gamepad_backend` and `gamepad_ignore`.

F10 toggles the FPS overlay live for the session without changing `settings.ini`.

### Bad values

Bad values are logged and ignored. See your UE4SS log for more info.

---

<a name="tech-notes"></a>
<p align="left" width="100%">
  <img src="https://raw.githubusercontent.com/modestimpala/VEmu/refs/heads/main/media/tech%20notes.png">
</p>

<details>
<summary>Click to read some technical notes about the mod</summary>
I never really thought I'd end up making an entire libretro frontend for this mod, but that's basically where it's at. There are only a handful of features it's still lacking, to name a few: ?

For rendering, it started with "can I get a SNES ROM displayed in-game?" Game Boy and SNES era video is cheap to render - your CPU can do it without breaking a sweat. I started by passing properly formatted pixel data to one of the game's plugins that converts it into a Texture2D. 

This eventually grew into a more complex engine integration that did direct render-thread texture uploads via vtable injection into UE4's RHI, bypassing the BP plugin to avoid extra copies. Hardware cores like mupen64plus got an offscreen OpenGL context with the framebuffer pulled back via async PBO readback on the render thread. Things worked, but required careful threading work and workarounds for core teardown. Everything was driven from the main mod, with each core given its own CoreWorker thread.

Once I started diving into the more intense cores like PCSX2, things got hairy. The workarounds were for cores that would crash on teardown - and crashes in the mod meant crashes in the host game. I wanted to avoid that entirely, so I made an architectural change.

Thanks to things like libco fiber switching, MTGS sync waits, and other core-internal threading weirdness, I refactored into a mod DLL + corehost EXE pair. The mod DLL dispatches corehost processes that handle all the libretro frontend work - loading a core, loading a ROM, dispatching retro_run. The two processes communicate via D3D11-pivot shared textures (via NT handles and keyed mutexes), IPC pipes for control, and shared memory rings for audio and input.

End result: a zero-copy (or at most single-copy) GPU round-trip for video data, with all core crash weirdness contained in its own process. No matter what a core does internally, it can't take down the main game.

Overall, I'm very pleased with the results, and I'm more than delighted to share this with the community. Please enjoy.

</details>

<a name="troubleshooting"></a>
<p align="left" width="100%">
  <img src="https://raw.githubusercontent.com/modestimpala/VEmu/refs/heads/main/media/tsing.png">
</p>

**Game won't load / nothing happens when I insert the cart.**

Open `<votv>\WindowsNoEditor\VotV\Binaries\Win64\UE4SS.log` and search for `[VEmu]`. Common causes:
- Missing core DLL - check `cores\` for the right filename. The mod logs `manifest: skipping <rom> -- no core for .<ext>` when nothing matches.
- Missing BIOS - some cores need a BIOS in `system\`. Check `system\required_bios.txt` for the current state, and the [core's libretro docs page](https://docs.libretro.com/library/bios) for filenames.
- ROM file not where the manifest scanner expected - try Layout 1 (loose at root) as a sanity check.
- For a core whose `.info` file isn't shipped: either drop the `.info` into `cores/info/` (grab it from the libretro buildbot alongside the DLL) or use a per-cart `core.txt`.

**Black Screen / Audio but no video: Hybrid/dGPU**

Set libretrocpp_corehost.exe to 'High performance' in Windows -> System -> Display -> Graphics, restart the game, and re-insert the cartridge.

**Cover art didn't download.**

Check your internet, then delete `<cart-folder>\cart_auto.failed` (or `<rom-stem>.cover_failed` for loose ROMs) and reload. Or just drop your own `cart.png` next to the ROM.

**Cart shows up greyed-out in the dispenser.**

The system needs a BIOS that isn't in `system\`. Check `required_bios.txt` for the expected filename.

**Keys don't work in-emu but work in-game.**

You probably aren't "gated" on the device - interact with it (default `Left Click`) first. Gamepad bindings work without gating; keyboard ones need it (so `W` doesn't drive both your character and the d-pad).

**I don't know what a given button does in this game.**

Check `keymaps\_descriptors\<system>.<rom>.txt` - the core writes what each RetroPad button means for this specific game.

**My emulator games lag**

Try disabling V-Sync, lowering settings, or trying lower-performance cores (SW cores like snes9x)

**My inputs/audio are delayed or the emulator plays weird**

Limit VotV FPS to ~60-120. 

---


<a name="legal"></a>
<p align="left" width="100%">
  <img src="https://raw.githubusercontent.com/modestimpala/VEmu/refs/heads/main/media/legal.png">
</p>

VEmu ships **no cores, no ROMs, and no BIOS files**. You bring your own.

- Cores are GPL/MIT/etc. licensed builds from the libretro project - see each core's license.
- ROMs/BIOS files are your responsibility. Dump your own; don't pirate.

---

<a name="credits"></a>
<p align="left" width="100%">
  <img src="https://raw.githubusercontent.com/modestimpala/VEmu/refs/heads/main/media/credits.png">
</p>

- Huge thanks to Libretro and core developers
- Shoutout to the UE4SS team (the framework that makes any of this possible)
- MrDrNose for The Game. 
- The Thunderstore team for the modding infrastructure that makes this distribution possible

## Model credits:

- PSOne, PSOne Controller, and CD/Jewel Case models created by **Viru**. 

- [GameToy](https://skfb.ly/pHwHD) model by cobracso is licensed under [Creative Commons Attribution](http://creativecommons.org/licenses/by/4.0/). 

- [SGES](https://skfb.ly/ovtIX) model by Manny Ruiz is licensed under [Creative Commons Attribution](http://creativecommons.org/licenses/by/4.0/). 

- [SGES Zapper Light Gun](https://skfb.ly/6RGWW) model by Matt Wilson is licensed under [Creative Commons Attribution](http://creativecommons.org/licenses/by/4.0/). 

For every CC-BY model, textures were edited to change style and text. Models were also resized or transformed to fit spec. 


## Super Epic Beta Testers:

- milk - early testing, keymap fixes 

- Viru - early testing, keymap fixes 

- Jake_489 - audio latency fix

- Mohl - early testing, audio/input latency fixes

- Robeebert - dx11 crash fix, ps2 l2/r2 input fix

- Valkyria Hammerlocke - ps2 l2/r2 input fix