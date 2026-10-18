# 1.1.0

## New

### Graphics
- **Smoother games.** About a quarter of some game's frames never reached the TV whenever VotV and the game ran at different frame rates, which showed up as stutter/micro hangs. Every single frame now gets through.
- **Steadier picture.** When VotV and a game run at the same frame rate (VotV capped at 60, a 60 fps game), the game's frames are now timed to land between VotV's frames, so they stop alternating between a repeated and a skipped frame. Recovering from a hitch no longer makes the game sprint for a moment.
- **Emulator GPU priority** (Settings > Emulator GPU priority, or `gpu_priority` in settings.ini). If a game slows down in heavy scenes while VotV stays smooth, Above normal or High lets the game's frames use the graphics card first. Normal by default.

### Audio
- **Less audio delay.** Sound now trails the picture by roughly 75 ms less (new defaults `pre_buffer_kb = 8`, `mixer_buffer_frames = 512`). If you hear crackling, raise `mixer_buffer_frames` to 1024 on the Settings page, or `pre_buffer_kb` to 16; UE4SS.log warns when the audio cushion runs dry.
- **N64 sound no longer lags behind the picture.** Some N64 games (maybe other cores too) played their sound up to a second late; any build-up of old sound is now dropped after a second.
- **Cleaner audio.** Volume above 100% no longer distorts, a momentarily late batch of audio no longer leaves a tiny gap, and recovering a console whose sound stopped no longer replays a burst of old audio.

### Controllers
- **Light gun keys don't take keys away from your games.** The gun's buttons (Enter, Y, G, B, I, N and U/H/J/K) only act while you're holding the gun, so those keys keep working normally in games the rest of the time.


# 1.0.0

- **F9 now opens the quick menu**, and **F10** shows or hides the FPS counter.
- **Save states are now compressed**, and old ones still load just fine.
- **Your consoles pick up where you left off.** When you save Voices of the Void (or quick/autosave), every console that's running a game is saved too. When you load that save, each one boots straight back into its game. Settings > Resume delay sets how long a game starts up before it jumps back to where you were.

## New

### Consoles
- **PlayStation**, with its own controller. It plays games from discs instead of cartridges. These awesome models were created by community member **Viru**.
- **Light gun.** The SGES Zapper plugs into a console like a controller. Aim it at the TV the console is connected to and click to shoot: you point at the actual screen in-game. Supports light gun games on NES (Duck Hunt and friends), PlayStation (Time Crisis and other GunCon games), Saturn (House of the Dead and other Virtua Gun games) and Dreamcast. Shooting off the screen reloads. The gun's buttons are on T, Y, G, B, I and N, with U/H/J/K as a d-pad, keys the base game doesn't use.

### Games and discs
- **Discs**, **jewel cases** and a **jewel case rack** to store them on.
- **Rewind.** Hold R to go back in time. Only works on cores with fairly small save states, so not Dolphin, PCSX2 and similar.
- **Multi-disc games.** Put all the discs of a game in one folder. To swap discs, take the disc out of the running console and put in the next one, just like the real thing.
- **Jewel case artwork.** Cases get a back cover and disc label, either from your own image files or downloaded automatically. Multi-disc games are labelled "DISC 1 OF 3" and so on.
- **Saturn games use Beetle Saturn by default**, which supports the light gun.
- **.7z files** work the same as .zip files.
- **Arcade games load correctly.** Zipped arcade games (FBNeo, MAME) were being unpacked when they shouldn't have been.
- **Clearer error messages.** If a game won't start, won't load or crashes, a hint popup tells you which system it was and why.
- **Easier BIOS setup.** `REQUIRED_BIOS.txt` in your system folder now starts with a list of what's missing, marks each file as found or missing, and gives the exact place to put each one. PS2 BIOS files are now detected correctly.

### Controllers
- **Any controller works**, including PlayStation, Switch and most generic USB or Bluetooth pads. Before, only one Xbox controller worked.
- **Up to four players.** Each controller you connect becomes the next player, and the game remembers which slot each controller had. A message pops up on the console when a controller connects or disconnects.
- **Rumble.** Games that support rumble now shake your controller. You can set the strength or turn it off. For N64 games, you may have to set the core's Player 1 Pak to "Rumble" in the quick menu.
- **Motion controls.** Games that use tilt or a gyro can read your controller's motion sensors, if your controller has them.
- **Gyro aiming.** Turn the controller to aim, like Steam Input's gyro aiming. You can aim all the time or only while you hold a button. In Wii games this moves the Wii pointer, and it works with a Nunchuk attached.
- **Tilt as buttons/sticks.** You can bind tilting the controller left, right, forward or back, or shaking it, to any button. You can also use tilt as a stick.
- **Rotate controllers in your hand** by holding right mouse button. Hold Shift or Alt with it to move the controller instead. It works just like the GameToy.
- **The controller in your hand moves with your real one** (optional, off by default). Tilt your real controller and the controller in the game tilts too.
- **Layouts for more systems:** GameCube and Wii, PSP and Mega Drive, plus keyboard controls for 25 systems that had none.
- **GoldenEye 007 comes with a twin-stick layout.** One controller plays it like a modern shooter.

### Quick menu (F9)
- **Redesigned.** The menu looks the same at any resolution and is easier to read, with even more info.
- **Save/Load shows a preview** of each slot, with a screenshot and the time you saved.
- **Controllers page.** Choose which controller is which player, make a controller rumble to find out which one it is, and set rumble strength.
- **Controls page.** Rebind any button or key while you play, for this game only, for every game on the system, or for the frontend shortcuts. Each player can have their own controller layout.
- **Settings page.** Change common settings without editing a file. Each setting tells you whether it takes effect right away, on the next game or after a restart.
- **Per-game options.** Core options can apply to every game, or to just the game you're playing.

### Everdrive
- **New demo/cracktro scenes.** An oldskool intro, a keygen screen before each game and a demo screensaver. Any button skips them, and you can turn them off in settings (Start/Home).
- **Customizable.** Add your own scroller fonts, scroll text and greetings in `%LOCALAPPDATA%\VEmu\everdrive\`. Music now plays .mod as well as .xm.
- **System tabs scroll** when you have lots of systems.

### Cart Dispenser
- **Much faster with big libraries.** Simpler filter buttons, and a list that only draws what's on screen. With a 2000+ game NES library, FPS went from about 40 to over 110.

### Graphics
- **Direct core Vulkan and Direct3D 11 support.** Cores that can use Vulkan or D3D11, such as Dolphin and PCSX2, can now render with them. A graphics setting lets you choose Auto, OpenGL, Vulkan or D3D11. Auto works for most people. If your graphics card can't run Vulkan, the game falls back to OpenGL.
- **No more freeze when you insert a game.** Games load in the background, so the game keeps running while a big PS2 or GameCube game starts up.
- **More cores work**, including N64 cores that need Vulkan.
- **Changing a game's internal resolution mid-game** now gives a sharper picture, instead of shrinking it to the old size.
- **Vertical (rotated) games** are shown the right way up.
- **The FPS counter** shows the real frame rate.

### Audio
- New audio effects in the quick menu's audio filter page: Bitcrusher (8-bit or subtle), Overdrive (warm or heavy), Hall and Room reverb, and a pitch shift.
- Smoother sound at the lowest resampler quality.
- Fast-forward can play sound now (sped up, like a tape): Settings > Fast forward sound. Off by default.

## Fixed
- Dolphin (GameCube/Wii): fixed graphics artifacts, missing audio, frozen pictures, and crashes when starting a game or changing resolution.
- N64: fixed crashes when saving, loading or ejecting, fixed games that ignored all input, and fixed the default button layout.
- Large GameCube and Wii save states no longer fail to load.
- Save-state screenshots are saved again.
- Some core options showed up as on/off switches when they had other choices.
- Messages from the game (resolution changes, menu actions) sometimes took up to 10 seconds to appear.
- A controller could control a console that nobody was holding.
- Unpacked disc images used to pile up in your temp folder. They're now cleaned up.
- Enabled CCD on Plugs and CDs, fixing an issue where they would fall through the map. 
- Fixed issues ejecting cartridges from consoles. Grabbing a cartridge or disc out of a console now puts it straight into your hands, instead of popping it out onto the console.
- Fixed a disc sometimes vanishing when you grabbed it and moved quickly, leaving the game running with no disc in the console, and a second disc then fitting in on top.
- Saturn and other CD games kept as separate track files no longer boot to an empty drive.

# 0.9.9

### In-game Quick Menu (press F10)

- Pause overlay over any running game. Change core options, toggle cheats, pick an audio effect, save/load states, swap discs, reset, and set fast-forward speed.
- Scales from Game Boy up to PS2.

### Cheats

- Drop RetroArch `.cht` files into your cheats folder; matched to games by ROM name (Game Genie / GameShark / Action Replay supported).
- Toggle cheats from the Quick Menu. Choices are remembered per game and re-applied after reset.

### Video

- Faster software-core video: rewritten color conversion (SSE2) gives roughly 4-6x higher throughput and lower per-frame CPU.
- N64 video appears correctly with smoother frame handling and one less full-frame processing pass.

### Audio

- New higher-quality "sinc" resampler. Set `[Audio] resampler = sinc` in settings.ini (`linear` remains the fallback).
- Audio effects (DSP): echo, reverb, EQ, chorus, phaser, tremolo, vibrato, wah, and more. 18 presets ship in `dsp\`. Pick one live from the Quick Menu or set `[Audio] dsp_preset`.
- Faster internal video color conversion (SSE2) for lower per-frame CPU on software cores.

### Controllers

- PlayStation now boots as a DualShock by default; analog sticks work immediately. Digital-only games unaffected. (Force digital pad with `port0 =` under `[devices]` in `playstation.ini`.)
- PS2 triggers (L2/R2) now report real analog pressure.
- Analog invert / sensitivity: add `:value` to a stick binding, e.g. `Gamepad_RightY = Stick_R_Y:-1.0` (invert) or `Stick_L_X:0.5` (half sensitivity).
- New `[devices]` aliases: `dualshock`, `analog_controller`, `guncon`, `justifier` (PlayStation), alongside Wii / GameCube.

### Fixes

- Fixed a recurring DirectX 11 crash (in nvwgf2umx.dll, common on NVIDIA). The per-frame video copy now runs on the render thread. Also plugged GPU memory leaks on cart insert.
- Fixed PS2 L2/R2 reading as dead (Square button driving both triggers) on some games.
- Fixed non-ASCII paths via UTF-8 application manifest and updating file handling
- Fixed the AV cord on SGES not re-binding to TVs on load

### New setting

- `[Paths] user_data_dir` - relocate the entire VEmu user-data folder (cores / roms / saves / etc.) off C: or next to the mod. Launch-time only.

# 0.9.8

- Audio is now in sync with video!
    - Emulator audio was running roughly 0.4 seconds behind the video, and that delay is now almost entirely gone.

### New & changed settings

- mixer_buffer_frames (new, default 1024) - Controls how much audio is buffered before it reaches your speakers. This is the main latency lever now.
    - Lower it (e.g. 512) for even less delay if you have a fast PC.
    - Raise it (2048 / 4096) if you hear any crackling or popping.
- pre_buffer_kb default lowered 32 -> 16 - Less audio delay out of the box. This is your safety cushion against audio hiccups, so if you're on an older CPU or running multiple emulator devices at once and hear occasional crackling, set it back to 32. Latency focused users: try 8 or 4.


 - Settings file now auto-updates
    - When an update adds new options, they're now automatically appended to your existing settings.ini

# 0.9.7

- Improved Everdrive menu; added alphabetical jump with L1/L2, title marquee scrolling, fixed 4096 rom limit
- Joypad input fixes

# 0.9.6

- Added Everdrive - a special cartridge that lists and plays every ROM. Costs 500 points, from the dispenser. 
- Fixed GameToy cartridge collision not allowing Eject after inserting into GameToy
- Fixed Cartridge Dispener allowing player to interact from far distances
- Fixed some phys mats
- Tightened corehost shmem trust-boundary
- Fixed TV-cord not pushing tex after selecting channel
- Disabled Vulkan path entirely. Vulkan is effectively unsupported at the moment. (see readme)


# 0.9.5

- Rotated GameToy meshes to face proper direction when holding
- Tried to fix controller plug reset issue. Disabled cable collision. Not perfect but less destructive.
- Fixed being unable to pick up cartridges after mounting in device.
- Fixed Emu Pause/Unpause.
- Hybrid/dGPU fixes: changed SharedD3D11Texture creation to pin the D3D11 device host adapter based on the LUID, avoiding video_sink.Init failed errors.
- Added backoff logic for hook registration retries, improving performance when the LibretroCpp pak is not installed.
- Added basic Vol Up/Down on device base.

# 0.9.4 

- Fixed SGES Controller store entry for REAL this time

# 0.9.3

- Reworked Shared SPSCR Audio ring to avoid bad audio and use-after-free
- Fixed default ROM being set to my own test games
- Made mounted cartidges unable to be held. You must press E on them to eject right now.

# 0.9.2

- Fixed SGES Controller arriving as GameToy from the store. Now arrives as the controller as it should.
- Changed default mupen/n64 core options and keymaps. Delete n64.ini / mupen*.opt to get upstream changes.

# 0.9.1

- Migrated user data to %APPDATALOCAL%\VEmu\ to avoid Thunderstore folder deletion wiping user files.

# 0.9.0

- Initial release