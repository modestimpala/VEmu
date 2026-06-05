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