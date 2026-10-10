## 2026-10-10 - Fire startup repeats redundant neighbor scans
**Learning:** Each `FireStreak` startup calls `FireEmitter.DoSoundAndLight`, which scans colliding fire actors in a 1024-unit radius. The sound/light decisions only depend on whether each count is zero, but the old loop also traversed every match and computed an unused distance; repeated streak creation during ignition can multiply this work.
**Action:** In this scan, stop as soon as both counts are nonzero and avoid restoring per-neighbor work that does not affect the final zero/nonzero decisions.
