# NES ROM Improvements

A starting point for improving performance and adding quality-of-life features to existing NES games. These techniques come from the Metroid performance patch. Each game needs its own timing measurements, ROM and RAM layout, and regression tests.

## Techniques to evaluate

| Metroid improvement | How to apply it to another NES ROM |
| --- | --- |
| **Synchronized sprites and scrolling** | Check whether the main loop finished before transferring sprites or updating the camera. If it missed the deadline, hold the previous sprite and scroll state together while keeping audio on schedule. |
| **Faster PPU update loops** | Choose the update mode once per block. Use separate loops for literal bytes and repeated values to avoid a mode check before every PPU write. Look for the same opportunity in games with buffered tile updates. |
| **Less room-buffer initialization** | Skip clearing regions the room builder is guaranteed to overwrite. Compare every room and destination buffer with the old routine, including attribute data and partially drawn rooms. |
| **Reuse room-building metadata** | Cache lookup addresses or other setup data shared by consecutive rooms. Rebuild the cache when its source tables change, such as during an area or graphics-bank switch. |
| **Battery saves using existing passwords** | Store the generated checkpoint and load it through the existing validator. Reserve cartridge RAM that survives the boot clear and keep ordinary START independent of the save slots. Verify that the emulator or cartridge hardware persists the data across a full restart. |
| **Guard drop retries and replenish renewable drops** | Check whether an item can be awarded before retrying a drop. For respawning enemies, tie repeatable pickups to enemy-slot availability or pickup lifetime so a room-wide cap does not permanently exhaust the source. |
| **Refill resources after a checkpoint load** | Once the game restores inventory and capacity, refill energy and ammunition through the normal initialization path. Test special passwords separately to preserve their original behavior. |

## Measure before changing the ROM

1. Record the ROM revision and checksum, mapper, emulator or hardware, and test inputs.
2. Pick a repeatable scene that exposes the problem. Measure missed game updates, main-loop headroom before the next NMI, and the time between the last video write and the end of VBlank.
3. Change one routine and replay the same inputs. Compare displayed frames and gameplay state at equivalent game updates. Treat debugger-assisted fixtures and normal gameplay as separate evidence.
4. Report timing, visual behavior, and gameplay outcomes independently. In Metroid, the NMI change kept sprites and scrolling together on missed frames, and room-loading changes reduced CPU cost. Some tested routes still missed updates.

[Metroid implementation, patching guide, and benchmarks](https://github.com/hydek12/MetroidNESPerformancePatch/blob/e91b14fc3c8d534ffea442790b81e2ce202b151a/README.md)
