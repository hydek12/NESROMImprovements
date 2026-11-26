# Agent guidance for NES ROM improvements

Follow [the standing agent rules](STANDING-AGENT-RULES.md) for all work in this repository. Use the [NES improvement techniques and measurement workflow](README.md) to decide which changes fit each game.

- Identify the exact ROM revision and checksum, mapper, and emulator or hardware. Record a repeatable baseline before proposing a patch.
- Inspect the game's frame loop, PPU updates, banking, and RAM ownership before adapting a technique. For timing fixes, measure missed updates, main-loop headroom, and VBlank video writes separately. Preserve sprite and scroll consistency and keep audio on schedule.
- For room-loading changes, verify tile and attribute buffers against the original across all affected rooms and destinations. Verify cache invalidation wherever lookup data can change.
- For saves and checkpoint changes, preserve the game's normal START and special password behavior. Verify persistence after a full exit and relaunch on the intended target. Check that pickup caps and retry paths preserve valid drops.
- Keep original ROMs and extracted game assets local. Publish reproducible patch tooling, compatibility hashes, and patching instructions.
