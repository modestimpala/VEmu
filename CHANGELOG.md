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