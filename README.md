# kernel-anticheat-lab

A research and learning project exploring kernel-level anti-cheat techniques for competitive FPS games.

This repo builds three things end to end:

1. **A Windows kernel driver** that observes and protects a game process (handle filtering, process/module/thread monitoring, integrity checks).
2. **A user-mode service** that bridges the driver and the game server over IOCTLs.
3. **An authoritative game server** (with a minimal test client) that validates player behavior and flags statistical anomalies.

> ⚠️ **Educational project only.** This is built to learn Windows internals, kernel driver development, and anti-cheat concepts — not to protect or attack any real, shipped game. Test only against the sample game included in this repo, and only on your own machines/VMs.

## Why this exists

Competitive FPS anti-cheat sits at the intersection of OS internals, security, and networked game design. This project works through that stack layer by layer: from a PE parser and a basic driver, up to process/handle monitoring, through to server-side statistical detection.

## Project structure

```
driver/       Windows kernel driver (C, WDK)
service/      User-mode service bridging driver <-> game server
game/
  client/     Test game client
  server/     Authoritative game server
  shared/     Shared protocol/types
tools/
  pe-parser/      Standalone PE header parser (early exercise)
  ioctl-fuzzer/   Fuzzes this project's own driver IOCTL surface
  log-viewer/     Views driver/service telemetry
docs/         Design notes, threat model, phase write-ups
tests/        Test harnesses and cheat scripts for the lab game only
```

## Status

Early stage — see [`docs/plan.md`](docs/plan.md) for the full phased roadmap.

- [ ] Phase 0: C/C++ and Windows fundamentals
- [ ] Phase 1: Dev/debug lab setup (VM, WinDbg, test signing)
- [ ] Phase 2: Sample game + authoritative server
- [ ] Phase 3: Driver core (device object, IOCTLs, user-mode service)
- [ ] Phase 4: Process/handle/module monitoring
- [ ] Phase 5: Integrity checks + telemetry
- [ ] Phase 6: Server-side statistical detection
- [ ] Phase 7: Hardening + write-up

## Requirements

- Windows 11 (VM strongly recommended — kernel bugs mean blue screens)
- Visual Studio + Windows Driver Kit (WDK)
- WinDbg (kernel debugging over network or serial)
- CMake, a C++17 compiler for the game/server/tools components

## Building

Build instructions will be filled in as each component comes online (see per-directory READMEs once they exist).

## Safety notes

- Never load the driver outside a VM or a dedicated test machine.
- Enable test-signing and Driver Verifier during development.
- Treat every IOCTL input as untrusted, even though it's "your own" service calling it.

## License

See [LICENSE](LICENSE).
